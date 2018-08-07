
 Note: This document is a partial copy of the UMTSkeeper website for your
 convenience. The most current version can be found at this location:
 http://mintakaconciencia.net/squares/umtskeeper/. 
  
  
  Installation
  ============
  Requirements
  ------------
   To run the program, Python2 needs to be installed (it's made with 2.7).
 Python is packaged with many distributions by default. If not, it should be in
 your package repositories, or you can download it from here:
 http://python.org/download/. Be aware that Python3 is not necessarily backward
 compatible with Python2 code. It's likely that UMTSkeeper will not run with
 Python3 - I did not test it yet.
  
   UMTSkeeper uses the Sakis3G script by Sakis Dimopoulos to set up the modem 
 and connect to the net. Since the original author abandoned the project (and 
 the original website, sakis3g.org, is offline), from version 2.05, I decided 
 to include the Sakis3G script with the UMTSkeeper download (I am not afiliated 
 with Sakis Dimopoulos). I include the "binary free" version, yet the "bninary 
 inclusive" (including usb_modeswitch) will do as well, should you need that. 
 For further information on Sakis3G, get the website from the 
 Internet Archive Wayback Machine: http://web.archive.org/web/*/http://www.sakis3g.org/ . 
 Read the manual!
   An up-to-date Sakis3G is maintained by Brenton Edgar Scott on GitHub: 
 https://github.com/trixarian/sakis3g-source .
    
   I'll do the commands that have to be given as the root user (or superuser,
 the general linux system administrator), using the sudo program, which asks
 you for your own password every time and which is the standard way on freshly
 installed Ubuntu systems. On other systems you may type su to become root.
 (sidenote: to activate the root account on Ubuntu, define a password for it:
 sudo passwd)
   Also, for packet installation, I will use the apt-get command, which is
 standard on Debian based distributions (also various flavors of *ubuntu and
 Raspbian). On other distributions I assume that you are familiar with whatever
 packet installer it uses (yum etc.). 
  
  
  Upgrading from version 1.xx
  ---------------------------
   Version 2 is designed to be a drop-in replacement for version 1.xx. Anyway,
 make a backup of your files first, then extract the new program files into the
 version 1.xx program directory. Version 2.xx will first convert your
 umtskeeper.stat file to a new format and add a few items. The px*.png files
 are not needed anymore.
  
  
  Prepare
  -------
   UMTSkeeper and Sakis3G should reside in the same directory. In this example
 it's /home/mintaka/umtskeeper/ - a subdirectory of my home directory, where
 mintaka is my user name. Substitute mintaka with your own user name.
 (Alternatively, you can put it in any location you find suitable). Typing pwd
 will show you the exact location you are working in which you will need later
 when you automate things (thanks BigCowPi for simplyfying this procedure). 
  
   If you don't have internet on your target system yet, download and transport
 the file there. The archive contains a "readme" file with these instructions
 as well. 
   In a terminal, this will download the archive, check if you indeed obtained 
 the file from this site (see output!), extract the scripts, and make them 
 executable (input line-by-line): 
  
    cd ~
    pwd
    mkdir umtskeeper
    cd umtskeeper
    wget "http://mintakaconciencia.net/squares/umtskeeper/src/umtskeeper.tar.gz"
    md5sum umtskeeper.tar.gz
    tar -xzvf umtskeeper.tar.gz
  
   Also make sure that your system properly detects the modem. The usual type of
 modem will first register as a storage device to the system, containing a 
 Windows executable which installs the modem manager software (on Windows, that 
 is). On Linux, these devices may need to be switched to modem mode with the 
 program usb_modeswitch, which should be available in your packet repositories 
 (most modern distributions have it installed by default; if not, try 
 sudo apt-get install usb-modeswitch 
 before you go compile it yourself). There's also a "binary" version available 
 on the Sakis3G website which includes usb_modeswitch. Many modems are 
 pre-configured in usb_modeswitch to work out-of-the-box, so there's no more to 
 be done there. If your modem is not switched automatically then you can find 
 more on configuring usb_modeswitch on the usb_modeswitch site
 http://www.draisberghof.de/usb_modeswitch/ and its forum
 http://www.draisberghof.de/usb_modeswitch/bb/. 
  
  Ubuntu users: do not set up an automatic connect with the GNOME Network
 Manager because it interferes with Sakis3G. You will likely use a headless
 machine, therefore the NM will not be useful anyway, so consider to uninstall
 it. This might apply to other distributions as well, I didn't test. You can
 still set up your network connections in /etc/network/interfaces. To remove,
 type sudo apt-get remove network-manager. 
  
  
  Notes on the Raspberry Pi
  -------------------------
   Power demand: 3G modems draw quite a lot of current. Therefore you'll need 
 to attach it using a powered USB hub (which can also power the RasPi), or use a 
 regulated 5V power supply that can deliver at least 1A, attached to the power 
 pins at the GPIO header (the micro-USB power socket and associated polymer fuse 
 would be overloaded by that amount of current). For more information, refer to 
 the numerous tutorials on the net.

    Raspbian (ver. 2014-09-08)
    --------------------------
    usb_modeswitch and ppp are not installed by default.
    
     sudo apt-get install usb-modeswitch ppp

   Mode-switching problems: When booting with an attached USB modem, the device 
 may not be identified as mode-switchable (due to timing/slow boot of the modem 
 itself, I suspect). As a possible remedy, UMTSkeeper has an automatic reboot 
 function from 2.07 onwards. If this doesn't help, try to remove usb_modeswitch 
 and use the "binary inclusive" version of Sakis3G which comes with its own 
 usb_modeswitch (source: https://github.com/trixarian/sakis3g-source).
 
   Feedback wanted: if you know of caveats with other distributions, please tell me :-)


  First Run
  ---------
   The clever way is to first connect manually with Sakis3G in interactive
 mode. Sakis3G will give you hints for the options to use. Do it as root.
   Please be aware that you should NEVER run a downloaded script with root 
 privileges unless you are sure what you do and that you indeed got the original
 file from the original source (not some trojan from a spy-in-the-middle).
 Checking the MD5 
 (http://mintakaconciencia.net/squares/umtskeeper/index.html#download) can help 
 but doesn't make you secure. You have been warned.
  
   sudo ./sakis3g --interactive 
  
   Hint: if you are asked for APN user or APN password but you have none, enter
 "0". 
  
   If your connection works in interactive mode, unplug and re-plug your modem
 and try with UMTSkeeper with all the switches and options, also as root.
   For example (this is a single line, mind the quotes!): 
  
  sudo ./umtskeeper --sakisoperators "USBINTERFACE='0' OTHER='USBMODEM'
USBMODEM='12d1:140c' SIM_PIN='1234' APN='CUSTOM_APN' CUSTOM_APN='provider.com'
APN_USER='0' APN_PASS='0'" --sakisswitches "--sudo --console" --devicename
'Huawei' --log --silent --nat 'no'
  
   UMTSkeeper will stay running after this. To end it, press the key
 combination CTRL+C.
  
   When run for the first time some log files will be created, among them
 /var/log/umtskeeper.log (the main log file), umtskeeper.stat.html (HTML
 statistics file to view in your web browser), and umtskeeper.stat (the file
 which keeps the numbers for the next run). To view umtskeeper.log, best open a
 second terminal and use cat or tail to view its content. It should contain
 something like this: 
  
  cat /var/log/umtskeeper.log
  
  2013-07-23 12:16:05 Start: PID = 21338
  Main stats file not found.
  Main stats file is incomplete. This happens in rare cases when UMTSkeeper is
killed in the wrong moment. Trying to load backup file. This can cause slight
inacurracies in the statistics.
  Main stats file backup not found. Possibly this program is being run for the
very first time.
  2013-07-23 12:16:05 Start: interval=4*8s
  Monthly stats file not found, setting up a new one.
  Daily stats file not found, setting up a new one.
  Hourly stats file not found, setting up a new one.
  Internet status:
  Cell network: No modem plugged.
  2013-07-23 12:16:41 Internet connection is DOWN. Calling Sakis3G connect...
  Sakis3G cmdLine: nice ./sakis3g connect --sudo --console USBINTERFACE='0'
OTHER='USBMODEM' USBMODEM='12d1:140c' SIM_PIN='1234' APN='CUSTOM_APN'
CUSTOM_APN='provider.com' APN_USER='0' APN_PASS='0'
  Sakis3G says...
  E1550 connected to PROVIDER (13579).
  2013-07-23 12:17:14 Testing connection...
  2013-07-23 12:17:24 Success... we are online!
  
  
   Sidenote: You can watch the log flow by typing tail -f
 /var/log/umtskeeper.log if you like. End the watch with the key combination
 CTRL+C. 
  
  Lines 3 to 5 are normal for the first run when the main statistics file
umtskeeper.stat is not yet present. Such an output should only make you worry
if they happen with subsequent starts. Sometimes, UMTSkeeper is interrupted
just when it is in the middle of writing the stats file, which would be fatal.
For such (rare) cases, a backup of that file is kept.
  The lines 7 to 9 tell you that new statistics files have been created. These
are comma-separated-values files which you can import into your favorite
spreadsheet software to plot lenghty graphs etc. - these statistics are kept
until you manually delete them. The files are: umtskeeper.hourly.csv,
umtskeeper.daily.csv, umtskeeper.monthly.csv.
  In line 11, it says no modem plugged, which is OK if you have the usual type
of modem that first registers as a storage device to the system. The script
will wait until the device is switched to modem mode.
  Line 13 gives the commands that are being sent to Sakis3G. Use this for
trying manually if something doesn't work. Sakis3G is called under the command
nice which means that the program will run with lower priority. S3G is CPU
hungry so you want it to play nicely and not interrupt other running processes.
  Lines 15 to 17 show that the connection has been established.
  
  
   If you unplug your modem now and re-plug it again then the connection should
 be established automatically. Give usb_modeswitch and Sakis3G a little
 patience. 
  
  
  Automatic Start
  ---------------
   Last, you want to start UMTSkeeper automatically after boot. Put a line into
 /etc/rc.local like this (it's a single line which will make it run in the
 background and redirect screen output to an error.log file): /etc/rc.local has
 to be edited by the root user. Replace the path /home/mintaka/ in this example
 by the path you found out previously. 
  
   /home/mintaka/umtskeeper/umtskeeper --sakisoperators "USBINTERFACE='0'
 OTHER='USBMODEM' USBMODEM='12d1:140c' SIM_PIN='1234' APN='CUSTOM_APN'
 CUSTOM_APN='provider.com' APN_USER='0' APN_PASS='0'" --sakisswitches "--sudo
 --console" --devicename 'Huawei' --log --silent --monthstart 8 --nat 'no'
 --httpserver &>> /home/mintaka/umtskeeper/error.log & 
  
  
   A line for only logging transfer statistics on wlan0 would for example look
 like this: 
  
   /home/mintaka/umtskeeper/umtskeeper --logonly --log --silent --monthstart 14
 --iface 'wlan0' --httpserver &>> /home/mintaka/umtskeeper/error.log &
  
  
  Dynamic DNS updater and e-mail notification
  -------------------------------------------
   There are two ways of using DDNS with UMTSkeeper: either let it call an
 external command line tool (if your DNS provider has a proprietary protocol),
 or use the internal update methods. Two methods are currently implemented: one
 is for the "freedns" style method which uses only an URL with an update code,
 and the other is the so-called "Members NIC Update API", invented by dyn.com
 and widely adopted by other services. The updater has been tested with
 freedns.afraid.org, dyn.com (dyndns.com) and no-ip.com.
   The DNS updater must be configured by configuration file, as the
 configuration potentially contains sensitive data. See the sample config file
 for more information.
   Notice, that if you use the DNS updater together with the webserver then
 your transfer statistics will be more easily accessible from the internet. If
 you don't want this, you can obfuscate the server by using a port other than
 standard HTTP port 80 (default is 8000), or you can secure it by using the IP
 whitelist feature. By all means, if those transfer statistics contain sensitive 
 data (all human-generated traffic does!), *don't get them over public nets 
 without encryption*. Security is your responsibility, don't take this lightly. 
 Read my advice: http://mintakaconciencia.net/squares/umtskeeper/#secure
 
  UMTSkeeper can also notify you about IP changes by e-mail. This must be 
 configured by configuration file, as the configuration will contain sensitive 
 data.
  
  
  Uninstallation
  ==============
   Currently, UMTSkeeper does not have an uninstaller (just as there is no
 installer). To remove it without a trace, delete <span
 class="path">/var/log/umtskeeper.log</span> and the whole program directory,
 and any special HTML dirs and temp dirs you may have made. That should be all.
  
  
  
  Parameters and Customization
  ============================
  Configuration file:
  -------------------
   All configuration can be done with command line parameters or in a
 configuration file. UMTSkeeper will look for <progPath>/umtskeeper.conf (1).
 The configuration goes this way: (1) overrides the program defaults, and
 values in a config file given by the --conf <conffile> command line directive
 overrides (1). Further, any parameters given on the command line will override
 the values from the config files. An example config file
 (umtskeeper.conf.sample) is included in the package, along with a lot of
 explanation.
  
  
  Commands:
  ---------
  connect
	  Retry connecting for example if connecting was suspended by --sakismaxfails.
  resetmonth
    Manually reset the monthly transfer counter.
  resettransferstats
    Reset the transfer amount counters. This will not reset the rate counters.
  Data will be deleted without asking again.
  resetratestats
    Reset the rate counters. This will not reset the transfer amount counters.
  Data will be deleted without asking again.
  stop, quit, end
	  Any of these will terminate a running UMTSkeeper.
  
  
  Options:
  --------
  --log
    Log to file (default: don't log). See also: logfile.
  --logonly
    Do not connect to internet. Use this for only logging statistics on a
  connection. Recommended only for (W)LAN devices. (default: do connect)
  --noroot
    Force running without requiring root privileges. The default behaviour is
  that if writing to system dirs returns "permission denied", it switches to
  no-root mode. This means, that all temp files and logs will be stored in the
  program directory. This switch is the equivalent of setting the config
  variables conf['logFile']=progPath+'umtskeeper.log',
  conf['tempPath']=progPath, and conf['statFilePath']=progPath.
  --nostats
    Don't write statistics files. (default: write them)
  --htmlstats
    Generate a HTML page without the internal webserver running. The HTML file
  is by default written to the temp dirctory:
  /run/umtskeeper/umtskeeper.stat.html or
  /var/run/umtskeeper/umtskeeper.stat.html. If --htmlPath is given then the
  HTML file is copied there. (default: none)
  --silent
    Suppress screen output (default: verbose).
  --httpserver
    Run the internal webserver (default: off). See also --httpport.
  
  
  Parameters:
  -----------
  --conf </path/to/configfile>
    Specify a configuration file to use. For the order of configuration, look
  above. (default: none)
  --iface <iface>
    Network interface to monitor (default: ppp0).
  --nat <iface>
    Enable internet connection forwarding (NAT). <iface> is the name of the
  network adapter that connects to the internet. Often, this is ppp0 (look it
  up with ifconfig when the connection is up). Set to 'no' if no forwarding is
  required. (default: no)
  --testcycle <s> (formerly --interval)
    Test connection in intervals of s statistics cycles (1 cycle is about 4
  seconds). (default: 8).
  --sakismaxfails <n>
    Maximum of failed connection retries by Sakis3G in sequence until the
  program gives up (actually it tries twice in a cycle). This parameter should
  help to save on power, especially with battery driven machines. Sakis3G is
  CPU intensive. So, if for any reason (modem unplugged or other failure) the
  connection doesn't work then we'd better give up constantly trying. See also
  --sakisfaillockduration. (default: 4)
  --sakisfaillockduration <s>
    Duration (in seconds) after which we retry to connect after the maximum of
  failed connection retries was reached. See also --sakismaxfails. (default:
  300)
  --logfile "<file>"
    To specify an alternative log file (default: /var/log/umtskeeper.log). This
  implies the option 'log'.
  --devicename "<string>"
    Set device name (eventually needed for device reset, this should be a
  unique identifier containing only letters and numbers. Get it with lsusb
  (don't listen to what Sakis3G says).
    Example: lsusb may return the device name string: ZTE WCDMA Technologies
  MSM MF110/MF627/MF636. Any unique part of this name is ok to take as the
  device name. So, --devicename "MF636" would be appropriate here.
  --statfilepath "<path>" (formerly --statpath")
    Write statistics files to this location. (default: script path)
  --temppath "<path>"
    Specify alternative path for temporary files. The default is to make a
  subdirectory in /run/ or /var/run/ (whichever is found), which is a tmpFS
  (ramdisk) filesystem on most platforms, and therefore the contents are lost
  on shutdown.
  --htmlpath "<path>"
    Webserver path to copy the stats HTML file to. (default: empty - do not
  copy)
  --httpport <port>
    Port on which the internal webserver is listening. Setting the port implies
  --httpserver. (default: 8000)
  --limitday <limit>
    Set daily transfer limit. (in bytes)
  --limitmonth <limit>
    Set monthly transfer limit. (in bytes)
  --monthstart <day>
    Day of month when monthly count begins. This is typically the day on which
  your monthly contract starts.
  --sakisswitches "<switches>"
   Set switches to pass to Sakis3g.
  --sakisoperators "<operators>"
   Set operators to pass to Sakis3g.
  
  
  License and Disclaimer
  ======================
  This program is released under a double license:
  ------------------------------------------------
    Primarily, the Hacktivismo Enhanced-Source Software License Agreement
  (HESSLA), which can be found in full and with an additional statement about
  its objectives, at http://www.hacktivismo.com/about/hessla.php;
    and for compatibility reasons, the GNU General Public License (GPL), see
  http://www.gnu.org/licenses/.
  
  While the GPL contains the terms and conditions under which this software and derivative works thereof can be freely distributed, and thus is aimed primarily at software developers, the HESSLA, while granting the same rights and obligations to modify and distribute the software, contains additional terms that govern the use of this software. This makes the HESSLA function as a contract between the author and the user, rather than just being a copyleft agreement.
    In particular, the HESSLA contains objectives on security standards (section 9), the adherence of the use of the software to respecting human rights, political freedom and privacy standards (section 10), as well as special terms on the use of the software by governmental entities and governmental persons (section 14).
  
    For the purpose of including this software or portions thereof in GNU GPL licensed projects, this software is also licensed under the GPL. You may distribute this software or derivatives under the GNU GPL, provided that YOUR DISTRIBUTION IS ALSO SUBJECT TO THE HESSLA.
  
    The HESSLA; full text is included with LICENSE.txt
    --------------------------------------------------
    UMTSkeeper is free software: you can redistribute it and/or modify it
    under the terms of the
    Hacktivismo Enhanced-Source Software License Agreement (HESSLA)
    as published by Hacktivismo, either version 1, or prior, of the License,
    or (at your option) any later version.
  
    By using UMTSkeeper, you express that you read and understood this
    license agreement, and that you are a Qualified Licensee as laid
    out in section 0.8, at the time you use UMTSkeeper, meaning that
    you will not use this software for infringement of human rights or the
    right to privacy. You will not use this software for surveillance purposes
    or to otherwise spy on people, neither for doing any harm to a human being.
  
    UMTSkeeper is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
    Hacktivismo Enhanced-Source Software License Agreement (HESSLA)
    at http://www.hacktivismo.com/ for more details.
  
  
    GNU GPL:
    --------
    UMTSkeeper is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 2 of the License, or
    (at your option) any later version.
  
    UMTSkeeper is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.
  
    You should have received a copy of the GNU General Public License
    along with UMTSkeeper.  If not, see <http://www.gnu.org/licenses/>.
