# xmlvirshparser

Python script to parse the output of `virsh dumpxml` command captured with sosreport.

# Installation

## Using pip

        # Activate python virtual environment and type
        pip install xmlvirshparser

## Manual Install

        # Clone repo by typing 
        git clone https://github.com/ervikrant06/virsh_xml_parser.github
        
        # Create virtual environment
        
        # Python 2.7
        virtualenv ~/myvirtualenvs/xmlvirshparser

        # Python 3.5
        pyvenv ~/myvirtualenvs/xmlvirshparser
        
        # Activate virtual environment
        source ~/myvirtualenvs/xmlvirshparser/bin/activate
        
        # Install package using
	
        cd virsh_xml_parser
        python setup.py install

# Usage

	xmlvirshparser <xmlfile1> <xmlfile2> <xmlfile3>

  or run using wildcard

	xmlvirshparser <xmlfile*>

	# Example
	xmlvirshparser xml_file_00*

## Examples

   - Running for dpdk based instances. MAC addresses are obfuscated.

~~~
$ xmlvirshparser virsh_outputs/DPDK/virsh_-r_dumpxml_instance-00000*
+-------------------+-----------+--------------------------------------+-----------------+------------+--------------------------------------+-----------+--------------------------------------+----------+------------------------------------+
| name              | domain-id | instance-uuid                        | instance-name   | flavor     | image-id                             | iface-cnt | iface-details                        | disk-cnt | disk-details                       |
+-------------------+-----------+--------------------------------------+-----------------+------------+--------------------------------------+-----------+--------------------------------------+----------+------------------------------------+
| instance-0000005f | 1         | b01ac376-e49a-4058-bd74-6d02db8c72fa | vCSM            | csm_flavor | 7be39b0f-d669-4f66-965c-1c19a0505c97 | 3         | [[u'vhostuser', u'xx:xx:xx:2b:f7:2e' | 2        | [[u'file', u'vda', u'virtio', None |
|                   |           |                                      |                 |            |                                      |           | u'vhostuser', u'xx:xx:xx:05:b6:63'   |          | u'file', u'vdb', u'virtio', None]] |
|                   |           |                                      |                 |            |                                      |           | u'vhostuser', u'xx:xx:xx:5d:9f:12']] |          |                                    |
+-------------------+-----------+--------------------------------------+-----------------+------------+--------------------------------------+-----------+--------------------------------------+----------+------------------------------------+
| instance-00000033 | 3         | fd5b4a1a-cf84-44c2-b6d3-030cc69dab5f | vcpu_equal_rx2  | dpdk.s2    | 1e9f4b0f-4a77-4933-b8d6-4c339e37452c | 1         | [u'vhostuser', u'xx:xx:xx:db:d5:fd'] | 1        | [u'file', u'vda', u'virtio', None] |
+-------------------+-----------+--------------------------------------+-----------------+------------+--------------------------------------+-----------+--------------------------------------+----------+------------------------------------+
| instance-00000119 | 2         | de344e9e-f4c3-400c-a93c-cf3847c35b67 | vUGW_SPU_C_0067 | vEPC.spuc  | 04f968c3-dc22-4572-8175-63c2d46182a9 | 2         | [[u'vhostuser', u'xx:xx:xx:4a:1b:69' | 2        | [[u'file', u'vda', u'virtio', None |
|                   |           |                                      |                 |            |                                      |           | u'vhostuser', u'xx:xx:xx:c3:ef:97']] |          | u'file', u'hdd', u'ide', None]]    |
+-------------------+-----------+--------------------------------------+-----------------+------------+--------------------------------------+-----------+--------------------------------------+----------+------------------------------------+
~~~

   - Running for SRIOV based instances.

~~~
$ xmlvirshparser virsh_outputs/SRIOV/virsh_-r_dumpxml_instance-00000007 
+-------------------+-------------+--------------------------------------+---------------+--------------+--------------------------------------+-----------+------------------------------------+----------+------------------------------------+
| name              | domain-id   | instance-uuid                        | instance-name | flavor       | image-id                             | iface-cnt | iface-details                      | disk-cnt | disk-details                       |
+-------------------+-------------+--------------------------------------+---------------+--------------+--------------------------------------+-----------+------------------------------------+----------+------------------------------------+
| instance-00000007 | Not-Running | 87f3b39e-a033-4a6c-9014-7a84f11d163e | sriov_2VF_2   | sriov_flavor | a88f576d-bfe1-454f-ac95-5c9f3dc20699 | 3         | [[u'hostdev', u'xx:xx:xx:0d:fe:6f' | 1        | [u'file', u'vda', u'virtio', None] |
|                   |             |                                      |               |              |                                      |           | u'hostdev', u'xx:xx:xx:09:ed:97'   |          |                                    |
|                   |             |                                      |               |              |                                      |           | u'hostdev', u'xx:xx:xx:6c:d4:c5']] |          |                                    |
+-------------------+-------------+--------------------------------------+---------------+--------------+--------------------------------------+-----------+------------------------------------+----------+------------------------------------+
~~~

   - Running for tap interfaces:

~~~
$ xmlvirshparser virsh_outputs/OSP7_01805281/virsh_-r_dumpxml_instance-0000*
+-------------------+-------------+--------------------------------------+-------------------------------+-------------+--------------------------------------+-----------+------------------------------------------------------+----------+--------------------------------------------------------------------------+
| name              | domain-id   | instance-uuid                        | instance-name                 | flavor      | image-id                             | iface-cnt | iface-details                                        | disk-cnt | disk-details                                                             |
+-------------------+-------------+--------------------------------------+-------------------------------+-------------+--------------------------------------+-----------+------------------------------------------------------+----------+--------------------------------------------------------------------------+
| instance-00002374 | Not-Running | 64940445-c2db-4d7e-bf16-b26e64d7bf1f | linux-migrate                 | small.2GB   | 7d00245e-fbfd-4b04-b328-fb506230a42c | 1         | [u'bridge', u'xx:xx:xx:ed:a1:94', u'tap6ff0f1fa-2a'] | 1        | [u'network', u'sda', u'scsi', None]                                      |
+-------------------+-------------+--------------------------------------+-------------------------------+-------------+--------------------------------------+-----------+------------------------------------------------------+----------+--------------------------------------------------------------------------+
~~~
