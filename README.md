# ansible-role-lms-service
installs logitech media service for free and open source multiroom audio streaming

## How to use

add host to hosts.yml:
```all:
  children:
     lms: # logitech media server
       hosts:
         192.168.1.217:
           ansible_user: root
           logitech_media_service_version: "8.1.1"
           music_server_http_proxy: False
           music_server_group: "squeezebox"
           music_server_playlist_path: "/squeezelist"
```
           
create site.yml:
```---
- hosts: lms

  pre_tasks:
   - name: update apt cache
     become: yes
     apt: update_cache=yes
     changed_when: False

  roles:
    - ansible-role-lms-service
```
created folder: mkdir roles
check out the role into roles folder
``` 
  git clone https://github.com/andreasbehnke/ansible-role-lms-service.git
```      

run playbook:
ansible-playbook site.yml --limit 192.168.1.217
