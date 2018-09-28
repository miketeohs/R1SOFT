1. postconf reload
r1soft
2. yum install r1soft-cdp-enterprise-agent
3. systemctl enable cdp-agent.service
4. systemctl start cdp-agent.service
5. systemctl status cdp-agent.service
6. systemctl list-units | grep r1soft
7. r1soft-setup --test-connection
8. r1soft-setup --get-key http://10.111.53.206
9. r1soft-setup --list-keys
10. r1soft-setup --get-module  # need kernel-devel rpm packae
and r1soft-getmodule-1.0.0-67.x86_64
/lib/modules/r1soft directory
ln -s hcpdriver-cki-3.10.0-862.11.6.el7.x86_64.ko hcpdriver.o




