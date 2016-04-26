[![Build Status](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-pxe_config.svg)](https://travis-ci.org/CSC-IT-Center-for-Science/ansible-role-pxe_config)
ansible-role-pxe\_config
=========

Configures PXE

Requirements
------------

a hosts file that looks like this (please note that node1/node2 below are not used to populate the hosts file, only the pxe_name and int_ip_addr and ib_ip_addr):

<pre>

[compute]
node1 int_ip_addr=10.1.2.1 ib_ip_addr=10.2.2.1 mac_address=00:11:22:33:44:55 pxe=yes pxe_name=io1
node2 int_ip_addr=10.1.2.2 ib_ip_addr=10.2.2.2 mac_address=00:11:22:33:44:56 pxe=yes pxe_name=io2

[pxe_bootable_nodes:children]
compute

</pre>

Role Variables
--------------

intDomain: "fgci.csc.fi"

siteName: "io"

These are the defaults:
<pre>
hosts_file_pxe_group_to_populate: "{{ groups.pxe_bootable_nodes }}"
hosts_file_admin_group_to_populate: "{{ groups.admin }}"
hosts_file_grid_group_to_populate: "{{ groups.grid }}"
hosts_file_install_group_to_populate: "{{ groups.install }}"
hosts_file_login_group_to_populate: "{{ groups.login }}"
</pre>

By setting the above to "" we disable that group. So let's say you only want to populate the production group, set the variables like so:

<pre>
hosts_file_pxe_group_to_populate: "{{ groups.production }}"
hosts_file_admin_group_to_populate: ""
hosts_file_grid_group_to_populate: ""
hosts_file_install_group_to_populate: ""
hosts_file_login_group_to_populate: ""
</pre>


See defaults/main.yml for some examples

Dependencies
------------

   * currently tightly integrated with dhcp\_server and pxe\_bootstrap

      * https://github.com/CSC-IT-Center-for-Science/ansible-role-pxe\_bootstrapo
      * https://github.com/CSC-IT-Center-for-Science/ansible-role-dhcp\_server



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: ansible-role-pxe_config }


Result
------

The tests we run are in here: https://github.com/CSC-IT-Center-for-Science/ansible-role-pxe_config/tree/master/tests

They generate a hosts file that looks like this:

<pre>
10.1.100.1 io1 io1.int.fgci.csc.fi
10.2.100.1 io1-ib io1-ib.int.fgci.csc.fi
10.1.1.6 io-admin admin-node io-admin.int.fgci.csc.fi
10.1.100.1 io-grid localhost io-grid.int.fgci.csc.fi
10.1.100.1 io-install localhost io-install.int.fgci.csc.fi
</pre>



License
-------

MIT

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
