Hi there ✋!

We can use this ansible role to perform bulk registration to Red Hat Satellite/Capsule server by passing the hostname/IP list in inventory file.


Requirements
------------

To execute this role successfully, we need to pass below variable values. First, we need to ensure that either we want to use root user or non-root user on client system side.

&nbsp;

**_Variables are:_**
```
ansible_ssh_user: Enter ssh username (Present on client system)
ansible_ssh_pass: Enter ssh password to take the ssh
Hostname: Enter Red Hat Satellite/Capsule server hostname
Activation_Key: Enter Activation Key Name
Organization_Name: Enter Organization Name (In which you want to register host on satellite server)
```

&nbsp;
>There are three ways to perform bulk host registration to Red Hat Satellite/Capsule server using bulk-registration ansible role.
* [x] 🌏 We can define these variable values either globally(For all hosts) in "vars/main.yml" file.

* [x] 🖥️ If we want to pass the variable values for per host in inventory file, syntax should be as below in inventory file. 
 ```
[host_list]
client.example.com    ansible_ssh_user=SSH_USERNAME ansible_ssh_pass=SSH_PASSWORD Hostname=SATELLITE/CAPSULE_FQDN Activation_Key=KEY_NAME Organization_Name=ORG_NAME
```


If all hosts in a group share a variable value, we can apply that variable to an entire group at once.
```
[host_list]
client1.example.com
client2.example.com

[host_list:vars]
ansible_ssh_user=SSH_USERNAME 
ansible_ssh_pass=SSH_PASSWORD 
Hostname=SATELLITE/CAPSULE_FQDN 
Activation_Key=KEY_NAME 
Organization_Name=ORG_NAME
```

* [x] 👨‍💻 If we want to pass the variable values at the same moment of ansible role execution, we can use below ansible playbook.

```

- hosts: all
  gather_facts: no
  vars_prompt:
    - name: ansible_ssh_user
      prompt: Enter ssh username (Present on client system)
      private: no
      
    - name: ansible_ssh_pass
      prompt: Enter ssh password to take the ssh
      private: no
      
    - name: Hostname
      prompt: Enter Red Hat Satellite/Capsule server hostname
      private: no
      
    - name: Activation_Key
      prompt: Enter Activation Key Name
      private: no
      
    - name: Organization_Name
      prompt: Enter Organization Name (In which you want to register host on satellite server)
      private: no
      
  roles:
    - bulk_registration

```


&nbsp;&nbsp;

If you required any help, please feel free to reach out to me on email. Many Thanks 🙂



Author Information
------------------

Name: [Nikhil Jain](https://www.linkedin.com/in/mrnikhiljain)
&emsp;
Email: nikhjain@redhat.com
