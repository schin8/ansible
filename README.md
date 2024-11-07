<div align="center">
  <a href="https://github.com/github_username/repo_name">
    <img src="docs/images/logo.png" alt="Logo" width="100" height="100">
  </a>
<h3 align="center">CodeBlast</h3>
  <p align="center">
    This project is underway.<br/>
    I'm redoing my home lab by consolidating my ansible setup.
    <br />
  </p>  
</div>



### Directory Structure

The basic directory structure looks like this: for more information , read the doc [Files and Folders](docs/Files_Folders.md).

```
├── inventory 
├── docs
│   ├── images
├── playbooks
│   ├── db
│   ├── setup
│   └── tools
└── vault 
```

### Inventory

Create one or more inventory files for your lab; I'm using a mix of Raspberry Pis, Proxmox LXCs, and Proxmox VMS.  

Example lower environment `lower.yml`

```
---
all:
  children:
    pi:
      hosts:
        <pi1>.local:        
    lxc:
      hosts:
        <lxc1>.local:        
    homelab:
      children:
        pi:
        lxc:        
    databases:
      children:
        pi:
        lxc:   
   
  vars:
    ansible_user: <ansible username>
```

Example usage:

If I wanted to ping all my databases on my Pis.

```
ansible-playbook ping.yaml -i inventory/lower.yml --limit databases --limit pi
```



