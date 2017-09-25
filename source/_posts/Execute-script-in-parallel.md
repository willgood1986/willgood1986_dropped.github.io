---
title: Execute Powershell Script in parallel
date: 2017-09-25 06:22:46
tags: Powershell, Parallel
categories: Powershell
---

> Sometimes it would take much time to execute the script. We can improve it by executing in parallel. We can create a couple of runspaces and execute the script in each.

<!--more-->

### Use the following script to call script in parallel  
> Save the following script into a script

```
if (test-path variable:\psise)
{
    throw 'It must be run from powershell.exe and NOT powershell_ise.exe!'
    break
}

#Script adapted from threading code by Osin Grehan
#http://www.nivot.org/2009/01/22/CTP3TheRunspaceFactoryAndPowerShellAccelerators.aspx

# Max run spaces
$MaxRunspaces = 25

# Concurrent number
$ConcurrentNumber = 4

# create a pool of runspaces
$pool = [runspacefactory]::CreateRunspacePool(1, $MaxRunspaces)
$pool.Open()

Write-Host "Available Runspaces: $($pool.GetAvailableRunspaces())" 
$jobs = @()  
$ps = @()  
$wait = @()   

for ($i = 0; $i -lt $ConcurrentNumber; $i++)
{
    # create a "powershell pipeline runner"
    $ps += [powershell]::create()

    # assign our pool of runspaces to use
    $ps[$i].runspacepool = $pool

    # Replace the 'script.ps1' with your own
    $script = "Invoke-Expression -Command .\script.ps1" 

    #Write-Host $script

    # Assign Scripts to powershell object
    [void]$ps[$i].AddScript($script)
    
    # start job  
    $jobs += $ps[$i].BeginInvoke();  
      
    Write-Host "Available runspaces: $($pool.GetAvailableRunspaces())" 
      
    # store wait handles for WaitForAll call  
    $wait += $jobs[$i].AsyncWaitHandle   

}

 # wait 1 hour for all jobs to complete, else abort  

 Write-Host (Get-Date), Begin to work in background, please wait ...

 #$success = [System.Threading.WaitHandle]::WaitAll($wait, 600000)  
  
  ForEach ($handle in $wait)
  {
      $handle.WaitOne(36000000)
  }  

 Write-Host  (Get-Date), "All completed" 
  
 # end async call  
 for ($i = 0; $i -lt $connStrings.Count; $i++) {  
  
     Write-Host "Completing async pipeline job $i" 
  
     try {  
         # complete async job  
         $ps[$i].EndInvoke($jobs[$i])  
     } catch {  
         # oops-ee!  
         Write-Warning "error: $_" 
     }  
  
     # dump info about completed pipelines  
     $info = $ps[$i].InvocationStateInfo  
  
     Write-Host "State: $($info.state) ; Reason: $($info.reason)" 
 }  
  
Write-Host "Available runspaces: $($pool.GetAvailableRunspaces())" 
```

### Put the following into a script file and put it with the calling script  
> The following is a sample script

```
   for ($i = 1; $i -lt 10; $i++)
   {
       Write-Host Current index $i    
   }
```
