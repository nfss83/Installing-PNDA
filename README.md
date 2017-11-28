# Installing PNDA on OpenStack

1 - Install the OpenStack using the devstack

Use a clean installation from Ubuntu Server 16.04. Update and Upgrage the packages.

$ sudo apt update && apt -y upgrade

Install the git and clone the OpenStack

$ sudo apt install git

$ git clone -b master https://github.com/openstack-dev/devstack.git

To install the OpenStack-Devstack, create a local.conf file and run the following commands.

$ cd devstack

$ nano local.conf

Insert the contents:

[[local|localrc]]

RECLONE=false

GIT_BASE=https://git.openstack.org

LOGFILE=$DATA_DIR/devstack.log
SCREEN_LOGDIR=$DATA_DIR/logs

FLOATING_RANGE=192.168.123.0/24
Q_FLOATING_ALLOCATION_POOL="start=192.168.123.133,end=192.168.123.200"
PUBLIC_NETWORK_GATEWAY=192.168.123.248

Q_USE_SECGROUP=True
ENABLE_TENANT_VLANS=True
TENANT_VLAN_RANGE=1000:1999
PHYSICAL_NETWORK=public
OVS_PHYSICAL_BRIDGE=br-ex

ADMIN_PASSWORD=openstack
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
SERVICE_TOKEN=openstack

disable_service n-net
disable_service tempest
enable_service q-svc
enable_service q-agt
enable_service q-dhcp
