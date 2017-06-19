---
title: Read items under appsettings in CSharp
date: 2017-04-20 07:28:32
tags: 
   -appsettings
   -C#
categories: 
   -C#
   -Configuration
---

> In C sharp, we can define some items in the appconfig file, read them dynamically in run time. Here is a sample about reading items in the configuration files.

<!--more-->

### Add custom items under appsettings node

```
<appSettings>
		<add key="sender" value="rtest1-10@test.com"/>
		<add key="recipients" value="test@test.com;test1@test.com"/>
		<add key="credential_user" value="rtest10@test.com"/>
		<add key="credential_password" value="secret"/>
		<add key="smtp_server" value="smtp.test.com"/>
		<add key="ssl" value="true"/>
		<add key="port" value="587"/>
	</appSettings>
```
### Read configuration
```bash
  using System.Configurations

  ConfigurationSettings.AppSettings[i_itemName]
```
