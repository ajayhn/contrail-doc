==================
Most common issues
==================

VM booted without an ip
=======================
Likely causes:
  * VMI doesn't have a link to RI

Debugging `Checklist <vm-booted-without-ip/checklist>`_

VM not able to reach destination
================================

VM has floating ip but isn't able to reach out
==============================================
* Default Security Group should have 0.0.0.0/0 allow

VM is connected to router with SNAT but can't reach out
=======================================================

VM name is not getting resolved (vDNS)
======================================

Name is not getting resolved (linklocal configured)
===================================================
