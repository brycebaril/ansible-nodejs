ansible-nodejs
==============

Install node.js via ansible.

This is a pretty simple bash script that uses http://npm.im/n to install Node.js

How To Use
==========

Copy the `nodejs` bash script into a library folder adjacent to your ansible playbook. You can then define a task like this to install node.js on your provisioned hosts.

```
---
- hosts: myhosts
  user: deploy
  sudo: True
  vars:
    node_version: 0.10.8
  tasks:
    - name: Install node.js
      nodejs: version={{node_version}}
```

*version*

Version is required, and should be the desired Node.js version number. You can use a string recognized by n such as 'stable' or 'latest' -- but currently the script will consider it a failure (even though the install should work) due to how it checks for success.


Internally it isn't much more than a wrapper around http://npm.im/n -- if you don't have node.js at all, it will bootstrap a local install of node.js in /tmp, then use that local install to run n to install to the system.

If you have node, it simply uses n to install the specified version. It will install n globally if not already present.

Caveats
=======

This module makes no attempt to support anything other than 64 bit Linux for the initial bootstrap. Pull requests welcome!

NOTE
====

Python is considered good form for Ansible modules, but for now it was much easier to convert something I already had written in bash. It does the job, but I may some day convert it to Python in order to submit it to ansible.cc


LICENSE
=======

MIT -- See LICENSE file.