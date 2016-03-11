The purpose of this document is to illustrate the capabilities of
Contrail based virtual networking and explain how it is achieved.

At the end of this we would have built components of a 2-layer web app
on an openstack based system. To that end, where available, openstack
API/commands will be used and contrail-specific API will be used when
there is no equivalent in openstack.

The feature highlight progression will be in the sequence of
  * Simple network/VM boot and access via link-local ip.
  * Access via floating-ip.
  * Connecting networks via network-policy.
  * Source NAT using logical-router.
  * Loadbalancing through VIP and floating-ip on VIP.
  * Analyzer.
  * Service-Chaining using VM L2 and L3 based service,for
    specific type of traffic, chains of services
  * vDNS.
  * Link-local services including name resolution.
  * Heat and port-tuples.
  * PNF

Preparation work for creating projects and adding user to projects:
  * create a project tutorial-public, a project tutorial-project-1 and
    add admin user in admin role in both projects

Simple network create and VM boot:
  * Create a public network and launch a VM in it.
    + create a network called public-net, subnet 10.10.10.0/24
      with router:external True in project tutorial-public
    + launch a VM, public-vm-1 with nic net-id=<public-id>,
      it will get ip of 10.10.10.3
    + access it from hypervisor/compute using the link-local ip

Accessing via floating-ip:
  * Create a web-server network/subnet and launch a VM in it.
    * create a network called webserver-net in tutorial-project-1
    * create a subnet 1.1.1.0/24
    * create a port on webserver-net, it will get ip of 1.1.1.3
    * launch a VM, webserver-vm-1 using port created above
  * Create/associate floating-ip to webserver VM, update security-group
    accept 0/0 trafic.
    + allocate a floating-ip from public-net (10.10.10.4)
    + associate floating-ip to port of webserver-vm-1
  * Access from public-vm-1 to webserver-vm-1.

Connecting networks via network-policy
  * Create a database-server network/subnet and launch a VM in it.
  * Create network-policy db-allow with rule to allow only port 3306(mysql)
    from any network.
  * Associate db-allow to database-server network and web-server network.
  * Access port 3306 from web-server VM to database-server VM.

Source NAT using logical-router.
  * Create a snat-for-database logical-router, set external gateway
    and add database-server subnet to it.
  * From database-server VM public VM should be accessible (source NAT).

Loadbalancing
  * Create a web-vip-endpoint network/subnet
  * Pool create, member create, VIP create web-vip-1
  * Create/associate floating-ip to VIP
  * Access from public-vm-1 to web-vip-1

Service Chaining using VM

Analyzer

Link-local Service

Virtual DNS

Heat
