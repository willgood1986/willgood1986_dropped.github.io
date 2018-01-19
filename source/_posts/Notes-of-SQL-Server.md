---
title: Notes of SQL Server
date: 2018-01-19 15:19:17
tags: SQL SERVER
categories: SQL SERVER
---
> Add some common usage of SQL Server here for quick reference.
<!--more-->

### Enable OpenRowSet ###
```bash
   exec sp_configure 'show advanced options', 1
   reconfigure
   exec sp_configure 'Ad Hoc Distributed Queries', 1
   reconfigure
```
