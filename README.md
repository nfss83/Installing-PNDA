# Installing PNDA on OpenStack

## 1 Install the OpenStack using the devstack

Use a clean installation from Ubuntu Server 16.04. 

1.1 Update and Upgrage the packages.

$ sudo apt update && apt -y upgrade

1.2 Install the git and clone the OpenStack

$ sudo apt install git

$ git clone -b master https://github.com/openstack-dev/devstack.git

1.3 To install the OpenStack-Devstack, create a local.conf file and run the following commands.

$ cd devstack

$ nano local.conf

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

enable_service q-l3

enable_service q-meta

enable_service neutron

enable_service horizon

enable_service h-eng h-api h-api-cfn h-api-cw

enable_plugin heat https://git.openstack.org/openstack/heat

enable_plugin ceilometer https://git.openstack.org/openstack/ceilometer.git

#Cinder configuration

#========================================

CINDER_SECURE_DELETE=false

#Two minions by default will create 25GB size volumes, so make your that we have anough space for volumes

VOLUME_BACKING_FILE_SIZE=100000M

#Enabling Swift

#========================================

enable_service s-proxy s-object s-container s-account

SWIFT_HASH=66a3d6b56c1f479c8b4e70ab5c2000f5

SWIFT_REPLICAS=1

SWIFT_DATA_DIR=/opt/stack/data/swift

------------------------------------------------------------
