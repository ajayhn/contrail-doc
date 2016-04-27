===========================
Generic indispensable Tools
===========================
* bash subshell to compose $(<cmd-to-run>)
* sed http://www.grymoire.com/Unix/Sed.html
* awk http://www.grymoire.com/Unix/Awk.html
* netstat
  + E.g.
      netstat -anp | grep $(pgrep contrail-api) | grep LISTEN
      netstat -anp | grep $(pgrep contrail-api) | grep ESTABLISHED
* lsof
  + E.g.
      lsof -p $(pgrep contrail-api) | grep log
      lsof -p $(pgrep contrail-api)  | wc -l
      lsof -i :5998
* strace
  + E.g.
      strace -ttt -ffff -p $(pgrep contrail-api) -s 1024
      strace -ttt -ffff -p $(pgrep contrail-api) -s 1024 -e trace=network
      # strace following children with timestamp for network system calls into a file:
      strace -ttt -T -f -p 10553 -o cass-trace -e trace=network -e verbose=all -s 4096
* tcpdump
  + E.g.
      tcpdump -tt -ni any port 8082 -A -s 1024 -e -vvv
* watch
  + E.g.
      watch -n1 "dropstats | grep -v '  0'"
* timeout
  + E.g.
      timeout 60s tcpdump -ni any port 9100 -A -s 1024 | grep X-Contrail-Useragent
* dpkg
  + E.g.
      dpkg -l | grep contrail-config
      dpkg --extract /path/to/deb /path/where/to/extract
* apt-cache
  + E.g.
      apt-cache policy contrail-config
      apt-cache depends contrail-config
      apt-cache rdepends contrail-config


===========================
Contrail command-line tools
===========================
* contrail-status
* contrail-logs
* flow, vif, nh, rt, mpls
* ifmap-view
* curl -u <user>:<passwd> localhost:8095/<resource>s?detail=True | python -m json.tool | less

==========================================
Tools for third-party s/w used by contrail
==========================================
* pycassaShell
* zkCli.sh
* rabbitmqctl
* contrail-api-cli
