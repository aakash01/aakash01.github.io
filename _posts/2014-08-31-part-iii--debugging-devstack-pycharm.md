---
layout: post
title: "Part III - Debugging DevStack (with pycharm)"
description: ""
category: OpenStack
tags: [OpenStack, DevStack]
author: aakash01
---
{% include JB/setup %}

In this post I'll show you how to debug devstack (neutron) with pycharm. 

1. Install Pycharm . 

2. Create a new project : openstack

3. Add a new remote host : Tools -> Deployment -> Configuration 
	
![remote_host_1]({{http://aakash01.github.io}}/assets/images/remote_host_1.png)
-----------------------
<br/>
![remote_host_2]({{http://aakash01.github.io}}/assets/images/remote_host_2.png)

NOTE : add /data and /logs to  excluded paths

4. Sync remote with local and download all files from remote VM to your local . In Remote host panel -> download from here. 

5. Configure remote interpreter : Settings (`Ctrl+Alt+S`) -> Project Interpreter -> add remote 
  

![remote_interpreter]({{http://aakash01.github.io}}/assets/images/remote_interpreter.png)

6. Enable `Gevent compatible debugging` : Settings (`Ctrl+Alt+S`) -> Python debugger -> check Gevent compatible debugging

7. Start `./stack.sh` on devstack VM 
	- go to screen mode , `screen -x
	- go to neutron screen `q-svc` .
	- kill service `Ctrl+A` `K`. 

8. Create a new debug configuration on pycharm : Run -> EditConfiguration ->  Python . Set following values
	- Script : \usr\local\bin\neutron-server   (you can check the exact location from `/opt/stack/logs/stack.sh.log` file).
	- Script Parameters : --config-file /etc/neutron/neutron.conf --config-file /etc/neutron/plugins/ml2/ml2_conf.ini
	- Python interpreter: remote interpreter created in above step. 

![debug_config]({{http://aakash01.github.io}}/assets/images/debug_config.png)

-------------------------------------------------------
We can debug using remote debugger as well . I'll check it out and update the post

###Happy Debugging .