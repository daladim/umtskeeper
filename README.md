# UMTSkeeper

This tool monitors a cellular connection made though the Sakis3g script. It adds several features:

* Connect the modem automatically and re-connect whenever possible.
* Optionally, break the connection when a pre-set transfer limit is reached.
* Basic IPtables setup for NAT (forwarding a single internet connection to the internal network).
* Dynamic DNS (DDNS) update client to update with standard DDNS services. This is not limited to cellphone-type connections.
* Transfer statistics in HTML which can be served by its own tiny webserver or your external webserver of choice, or read directly from disk. This is not limited to cellphone-type connections.


## How it works
A detailled guide on installing and running UMTSkeeper is available in [INSTALL.html](INSTALL.html).


## Credits

Many thanks and most of the credit should go to Elijah el-Mintak, who developed this script until v2.07 and made it available on [http://mintakaconciencia.net/squares/umtskeeper/](http://mintakaconciencia.net/squares/umtskeeper/).

With his consent, I am now hosting this script on Github, and added a patch of mine on this occasion. Having this script on Github will now (maybe) have the community to extend it further.

I will be happy to review and merge any pull request!

## TODO

This tool has been working well since 2013. Yet some features could still be added, such as :

* Investigate running the thing as a real deamon, which should allow to run it
  without log-in on stand-alone headless systems. Install/uninstall,
  rc-scripts, logrotate.
* Probably make some more use of the webserver.
* Get connect/disconnect markers into the graphs.
* Get UMTSkeeper to work with NetworkManager
* Sakis3g is also an old (yet great) piece of software. Does it need a replacement?
