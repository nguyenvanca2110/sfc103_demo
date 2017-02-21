# sfc103_demo
SFC 103 demo

SFC103 Demo
===========

Overview
--------

SFC103 demo is to show standalone SFC classifier including dynamic insert
& remove service function.

Note
----

It takes long time to complete the demo including vagrant box download,
SFC download/build and ovs with NSH installation. The duration depends
On your network. Normally, it takes several hours.

Global Topology
---------------

                           +-----------------+
                           |       SFC       |
                           |   192.168.1.5   |
                           +-----------------+
                       /      |          |     \
                    /         |          |         \
                /             |          |             \
+---------------+  +--------------+   +--------------+  +---------------+
|  Classifier1  |  |    SFF1      |   |     SFF2     |  |  Classifier2  |
|  192.168.1.10 |  | 192.168.1.20 |   | 192.168.1.50 |  |  192.168.1.60 |
+---------------+  +--------------+   +--------------+  +---------------+
                              |          |
                              |          |
                   +---------------+  +--------------+
                   |     DPI-1     |  |     FW-1     |
                   | 192.168.1.30  |  | 192.168.1.40 |
                   +---------------+  +--------------+

Classifiers Topology
--------------------

            +---------------------------------+
            |            ARP Cache            |
            + - - - - - - - - - - - - - - - - +
            | 192.168.2.2 | 00:00:22:22:22:22 |
            +---------------+-----------------+
                            |
+---------------+           |
|               |-----------+------------+                  +-------+
|               | veth-app               +        +---------|       |
| Classifier1   | IP: 192.168.2.1/24     +        +         |       |
| 192.168.1.10  | MAC: 00:00:11:11:11:11 ++------++ veth-br |  app  |
|               | MTU: 1400              +        |         |       |
|               |------------------------+        +---------|       |
+---------------+           ▲                               +-------+
                            |
                            |
                            |
+---------------+           ▼
|               |------------------------+                  +-------+
|               | veth-app               +        +---------|       |
| Classifier2   | IP: 192.168.2.2/24     +        +         |       |
| 192.168.1.60  | MAC: 00:00:22:22:22:22 ++------++ veth-br |  app  |
|               | MTU: 1400              +        |         |       |
|               |------------------------+        +---------|       |
+---------------+           |                               +-------+
                            |
            +---------------+-----------------+
            |            ARP Cache            |
            + - - - - - - - - - - - - - - - - +
            | 192.168.2.1 | 00:00:11:11:11:11 |
            +---------------------------------+

Setup Demo
----------
1. Install virtualbox & vagrant(>=1.8.0) in ubuntu 14.04.03
2. Git clone the sfc103_demo script, then creat a new folder: sfc103
  git clone https://github.com/nguyenvanca2110/sfc103_demo.git
3. ./demo.sh


Cleanup Demo
------------
1. vagrant destroy -f


Trouble Shooting(TBD)
--------------------
Update for SFC-H
1. Don't use function start_sfc (run_demo.sh)
2. Don't start "Start Demo" 
//------------------------------------
echo "SFC DEMO: Clean"
clean

echo "SFC DEMO: Start SFC"
#start_sfc

echo "SFC DEMO: Build Docker"
build_docker

echo "SFC DEMO: Give some time to have all things ready"
sleep 120

echo "SFC DEMO: Start Demo"
#start_demo
//-------------------------------------
Vagrant Image for VirtualBox
https://www.dropbox.com/sh/dn53i99jm2x2wdg/AAAcRZWM_qCWRdCTWDw2PZS1a?dl=0

// Permission for sh file
(Do not recommend use "sh name.sh" to run scripts, because it maybe occur a lot of error)
sudo chmod +x name.sh
