Ansible role: win_msbuild
=========
[![Build Status](https://travis-ci.org/gmarokov/ansible-role-win-msbuild.svg?branch=master)](https://travis-ci.org/gmarokov/ansible-role-win-msbuild)

Ansible role for building and deploying ASP.NET site to IIS with MSBuild.

Requirements
------------
1. Include as a build step. Required MSBuild installed and your project's code repository checkout. 
3. IIS must running on target server and the site must be created.
5. Web Management Service must be installed, enabled and running at port 8172 on the target server.

Role Variables
--------------

`proj_path`
Full path to the site's parent directory. Role automatically enters the folder by `site_name` and finds the `.csproj` by that again. e.g.: `proj_path = "C:/Repo/Sites"` 

`site-name`
Project name in repository. Must be a project folder which contains `.csproj` with the same name.

`server_ip`
IP address for the target server where the site will be deployed. Get it from the inventory groups, as variable or other mechanism. 

`iis_site`
Site name in IIS.

`config`
Build configuration. By default is Release. Overwrite if needed.

`ansible_user` 
User for the remote session on Windows. Configure this in playbook or group_vars is preferred.

`ansible_password`
Password for the user on the Windows instance. Use vault, prompt or other secure schemas. 

Example Playbook
----------------

```
- role: win_msbuild
     vars: 
      proj_path: "C:/Repo/Sites/"
      site_name: "MyAspNetSite"
      server_ip: "{{ groups['webservers-stage'][0] }}"
      iis_site: "my-asp-net-site"
      config: "Stage"
     tags: 
      - site
```

License
-------

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

