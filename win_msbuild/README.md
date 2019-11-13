Ansible role: win_msbuild
=========

Ansible role for building and deploying ASP.NET site to IIS via MSBuild.

Requirements
------------
0. Windows build server with MSBuild installed and your project's code repository checkout
1. IIS must be up and running on target server
2. Site must exist in IIS on the target server
3. Web Management Service must be enabled and running at port 8172 on the target server

Role Variables
--------------

`proj_path`
Full path to where your project is. Role automatically enters the folder by `site_name` and finds the `.csproj` by that again. 

`server_ip`
IP address for the target server where the site will be deployed. Get it from the inventory groups or hard code it. 

`iis_site`
Site name in IIS

`config`
Build configuration. By default is Release. Overwrite if needed.

`ansible_user` 
User for the remote session on Windows. Configure this in playbook or group_vars is preferred.

`ansible_password`
Password for the user on the Windows instance

Example Playbook
----------------

```
- role: win_msbuild
     vars: 
      proj_path: "C:/MyAspNetSiteRepo/"
      server_ip: "{{ groups['webservers-stage'][0] }}"
      iis_site: "my-asp-net-site"
      site_name: "MyAspNetSite"
      config: "Stage"
     tags: 
      - site
```

License
-------

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

