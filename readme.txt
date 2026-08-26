This contains files and docs for using the Fortnet VPN from Ubuntu because USDA OCIO doesn't seem to be able to come up with a way for us to do it otherwise.

Compoonents:

OpenFortiVPN: https://github.com/adrienverge/openfortivpn This is the stuff that creates the VPN connection. I used it instead of Fortinet's official client because it was more straightf  and easier for me to figure out.

Issue for Openfortivpn that talks about the service: https://github.com/adrienverge/openfortivpn/issues/623

Creating services: https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6

For a full list of configuration options, see manFor the full list of config options, see the CONFIGURATION section of man openfortivpn; there are probably a lot I haven't looked at.

Configuraiton File: a file in this repo that contains parameters for openfortivpn.

NOTE: This is currently using Steve's FortiNet account.

systems file: The file that sets up a system service that can be used with to set up the server.

To start it:

sudo systemctl start openfortivpn@graingenes.service

You can have several VPNs with different names, by creating different configurations.

All the standard systemctl commands work.

systemctl status openfortivpn@graingenes.service
● openfortivpn@graingenes.service - OpenFortiVPN for graingenes
     Loaded: loaded (/lib/systemd/system/openfortivpn@.service; disabled; vendor preset: enabled)
     Active: active (running) since Wed 2026-08-26 13:59:12 PDT; 43min ago
       Docs: man:openfortivpn(1)
   Main PID: 3844 (openfortivpn)
      Tasks: 6 (limit: 77127)
     Memory: 4.1M
        CPU: 116ms
     CGroup: /system.slice/system-openfortivpn.slice/openfortivpn@graingenes.service
             ├─3844 /usr/bin/openfortivpn -c /etc/openfortivpn/graingenes.conf
             └─3850 /usr/sbin/pppd 230400 :169.254.2.1 noipdefault noaccomp noauth default-asyncmap nopcomp receive-all nodefaultroute nodetach lcp-max-configure 40 mru 1354>

Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3844]: INFO:   Negotiation complete.
Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3844]: INFO:   Negotiation complete.
Aug 26 13:59:23 ARSCAALB0GGDEV00 pppd[3850]: local  IP address 10.16.224.10
Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3850]: local  IP address 10.16.224.10
Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3850]: remote IP address 169.254.2.1
Aug 26 13:59:23 ARSCAALB0GGDEV00 pppd[3850]: remote IP address 169.254.2.1
Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3844]: INFO:   Interface ppp0 is UP.
Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3844]: INFO:   Setting new routes...
Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3844]: INFO:   Adding VPN nameservers...
Aug 26 13:59:23 ARSCAALB0GGDEV00 openfortivpn[3844]: INFO:   Tunnel is up and running.
