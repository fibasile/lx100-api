Remote control features

For all the camera control features, it's very easy to mimic the LL application : you just have to send GET http requests to the GH3 ip address. You can do that using your browser, for example if you try to go to http://@IP_GH3/cam.cgi?mode=camcmd&value=capture the GH3 will take a picture. You can open the file "requests.html", and you will find most of the possible commands.

An interesting improvement to the actual interface could be to only display the settings compatible with the mode you're in, and lens you use (PASM...mode, focus mode, left control dial mode, minimum/maximum aperture, ...).
this can be achieved easily by parsing the XML responses to the following HTTP GETs :

http://@IP_GH3/cam.cgi?mode=getinfo&type=curmenu : the answer to that is a xml file listing a lot of info about the actual state of the GH3. For example, if you're not in Program Mode, you will have :
item id="menu_item_id_program_shift" enable="no" somewhere. You just have to parse this xml file and do a few checks, and you will know exactly in which modes you're in.
http://@IP_GH3/cam.cgi?mode=getinfo&type=allmenu : a lot of interesting info here about a lot of commands, and all the GH3 menus in the different languages !
http://@IP_GH3/cam.cgi?mode=getinfo&type=lens : lens detected. The answer is a string, ie for the 14-42PZ it's "ok,2304/256,925/256,3072/256,16384/256,0,on,42,14,on,128/1024". I think this site could help us finding the info of all the electronic m4/3 lenses there is:)
A few applications could be possible using the different commands and writing a little javascript (electronic follow focus, advanced bracketing/time-lapse, ...) and I'm sure it could also serve some very specific, rare use cases.
Application ideas and developers are welcome

Liveview

If you go to http://@IP_GH3/cam.cgi?mode=startstream&value=49152, the GH3 will send an udp stream to your ip address on port 49152. The problem is it's not RTP, so after losing hours trying to find an known header pattern at the beginning of the udp data, I finally had the late idea to look at the last bytes : it is "ff d9". A rapid google search taught me that it was the EoF marker for jpg images. The stream is a MJPEG video over UDP. If you look at this hex dump file, you will find :

a 144 bytes "header" (with a few changing bytes, and a lot of repeating patterns in the different occurences of these headers / separators)
ff d8 ...... ff d9 : a jpg file
a 144 bytes "header"
ff d8 ...... ff d9 : another jpg file
and so on
Edit v04 : The "header" size actually change depending on several factors (autofocus, dial mode), but this is taken care of by the live view Java program.
You will find attached to that email the hex dump of a short video streamed by the GH3 (mjpegOverUdp.hexdump.txt.zip, the data payload of the UDP stream), and the pcap capture file of the session from which it has been extracted (mjpegOverUdp.zip).
Ideally, it will be better to understand what the changing bytes in the header/separator represent.

Picture preview/download

I didn't play much with this, but the GH3 and lumix link use the UPNP set of network protocols to communicate. More testing is needed to see what SOAP messages are exchanged when doing the few interesting actions on the LL app "Playmode". As an example, I attach to this email the SOAP message sent to the GH3 to have the list of pictures (ImageBrowse_requestLL.soap.txt), and the SOAP response of the GH3 (ImageBrowse_responseGH3.soap.txt).

If you want to go deep in the understanding of UPNP, see http://upnp.org/resources/upnpresources.zip
If you want some info about the GH3 upnp services, start here : http://@IP_GH3:60606/2002AFF26C52/Server0/ddd
If you want some info about the Lumix Link services, start here : http://@IP_LL:49152/dms/ddd.xml
