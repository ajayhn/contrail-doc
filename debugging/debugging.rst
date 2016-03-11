==================
Most common issues
==================

VM booted without an ip
=======================
**Likely causes**:
 + `VMI <../glossary.rst>`_ doesn't have a link to RI
 + `VMI <../glossary.rst>`_ 's configuration in database is not present downstream
    in control-node and/or contrail-vrouter-agent
 + Plug for vif was not received from nova-compute
 + DHCP is not enabled or not working 

Debugging `Checklist <vm-booted-without-ip/checklist.rst>`_

VM has floating ip but isn't able to reach out
==============================================
**Likely causes**:
  + default security-group for project doesn't have 0/0 allow ingress
  + default route in native RI is leading somewhere else
  + tunnel endpoint encapsulation is incorrect (MPLSoUDP instead of MPLSoGRE)

VM not able to reach destination
================================
**Likely causes**:
  + flow setup is not happening
  + flow entry is set to drop egress or ingress
  + L2 instead of L3(arp-cache poisoned) or vice-versa

VM intermittently able to reach destination
===========================================
**Likely causes**:
  + ip-address reused/shared by 2 ports leading to ECMP/asymmetric path
  + ip-address is of scale-out svc-instance and one of svc-vm is down/dropping

VM is connected to router with SNAT but can't reach out
=======================================================
**Likely causes**:
  + 0.0.0.0/0 route not present in routing-instance
  + SNAT netns not functional
  + multiple functional SNAT netns with pref 200(ECMP/asymmetric path)

VIP never/stopped working
=========================
**Likely causes**:
  + lbaas-haproxy netns not functional
  + multiple functional lbaas-haproxy netns with pref 200(ECMP/asymmetric path)

VM name is not getting resolved (vDNS)
======================================
**Likely causes**:
  + contrail-dns doesn't have configuration via ifmap for net/vdns/ipam
  + xmpp publish about endpoint not received
  + send to contrail-named(bind) failed
  + >2 contrail-dns active in cluster and different sets of 2 in use

Name is not getting resolved (linklocal configured)
===================================================
**Likely causes**:
  + dynamic port range in linux kernel incorrect

Project Name and UUID mismatch between keystone and contrail
============================================================
**Likely causes**:
  + Project in keystone deleted even though there were VM|VN|Policy
    and re-created with same name
