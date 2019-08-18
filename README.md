# gns3_auto_topology_builder

## Overview
    
   This repository contains a python3 script **[gns3_deploy_topology.py]**
   that is used to deploy a GNS3 topology from a YAML file using GNS3 API.
   
   The auto_builder can be useful in combination with CI/CD. For example, to build a development environment for a Network Engineer.
   
   The main idea was to do not open GNS3 GUI interface to communicate with devices and use it like a code because my GNS3 server is located far away from me [>=380ms.] and it was hard to use GUI interface.
   
   You can find some examples in [Examples](https://github.com/dmmar/gns3_auto_topology_builder/blob/master/Examples) and [NetasCode_example](https://github.com/dmmar/gns3_auto_topology_builder/blob/master/NetasCode_example) folders.
   
   **Tested on [GNS3 2.1.21] and appliances such as Cisco IOSv, IOSvL2, vASA 9.9.2, VyOS 1.1.8 and JunOS vSRX 17.3R1.**

   *The script does not support GNS3 server authentication login/pass for now.*
   
   **P.S. Author is not an expert, he is learning how to code. Errors can exist.**
   
   I would appreciate any feedback. Thank you!

## Prerequisites

    * python3
    * pip3
    * GNS3
    
## Getting Started

    # git clone https://github.com/dmmar/gns3_auto_topology_builder
    # pip3 install -r requirements.txt
    
## Running simple examples:

    The most important part is to get the right names of appliances from a GNS3 server.
  
    For that, you can use a simple python3 script which will show you all current appliances on your GNS3 server.
    Those appliances names you can copy and paste to the topology file (.yaml).
    * I have used mine appliances names and IP addresses to make these examples. For you they can be different.*
    
    Use the following to get appliances names/ids:
    # python3 gns3_show_appliances.py -s http://[<IP>:<port>]
    For example, # python3 gns3_show_appliances.py -s http://172.30.33.200:3080
    
    [Simple examples:]
    * Please, before run a script look at the topology file (.yaml) and the diagram (.png)
    Also, please read * Important notes section *
    
    # python3 gns3_deploy_topology.py -f Examples/ex1/gns3_simple_topology_1.yaml
    # python3 gns3_deploy_topology.py -f Examples/ex2/gns3_simple_topology_2.yaml
    # python3 gns3_deploy_topology.py -f Examples/ex3/gns3_simple_topology_3.yaml
    
## Running NetasCode examples:

    You can use these examples to deploy GNS3 topologies of the virtual fictional company 'X' and play with network automation.
   More information: https://github.com/dmmar/netascode
    
    [NetasCode examples:]
    * Please, before run a script look at the topology file (.yaml) and the diagram (.png)
    Also, please read * Important notes section *
    
    # python3 gns3_deploy_topology.py -f NetasCode_example/gns3_dev_topology.yaml
    # python3 gns3_deploy_topology.py -f NetasCode_example/gns3_test_topology.yaml
    # python3 gns3_deploy_topology.py -f NetasCode_example/gns3_prod_topology.yaml
    
## Important notes:
    
    - Running time for JunOS vSRX is 10 min.
    - Running time for VPCS is 5 sec.
    - Running time for other GNS3 appliances is 1 min.
    
    - Startup configs applies using [Netmiko with pexpect via telnet], and for Cisco IOS, ASA, JunOS, VyOS, and VPCS.
    For more information look at [def gns3_send_start_config_telnet()] in gns3_deploy_topology.py script.

    - global_delay_factor: 4
    
    # global_delay_factor for [gns3_send_start_config_telnet]
    # I have used a global delay parameter because
    # my GNS3 server is located far away from me (380>= latency).
    # info https://ktbyers.github.io/netmiko/docs/netmiko/

    
## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/dmmar/gns3_auto_topology_builder/blob/master/LICENSE) file for details.

