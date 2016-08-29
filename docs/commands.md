When you connect a device to the camera the camera will have this IP address:
192.168.54.1

Using you browser you can find all supported command by the camera:
http://192.168.54.1/cam.cgi?mode=getinfo&type=capability

Here are a few command with some explanation:

http://192.168.54.1/cam.cgi?mode=getstate – current state
http://192.168.54.1/cam.cgi?mode=setsetting&type=afmode&value=facedetection – set auto focus and facedetection

http://192.168.54.1/cam.cgi?mode=camcmd&value=recmode  = recording mode
http://192.168.54.1/cam.cgi?mode=camcmd&value=playmode  =  play mode
http://192.168.54.1/cam.cgi?mode=camcmd&value=capture – take picture
http://192.168.54.1/cam.cgi?mode=camctrl&type=touchcapt&value=840/234&value2=on – take a picture with focus on a given coordinate
http://192.168.54.1/cam.cgi?mode=camctrl&type=touchcapt&value=0/0&value2=off
http://192.168.54.1/cam.cgi?mode=camcmd&value=video_recstop  – stop recording video
http://192.168.54.1/cam.cgi?mode=camcmd&value=video_recstart – start recording video

http://192.168.54.1/cam.cgi?mode=camcmd&value=wide-normal – zoom in
http://192.168.54.1/cam.cgi?mode=camcmd&value=wide-fast – zoom in
http://192.168.54.1/cam.cgi?mode=camcmd&value=tele-normal – zoom in
http://192.168.54.1/cam.cgi?mode=camcmd&value=tele-fast – zoom in
http://192.168.54.1/cam.cgi?mode=camcmd&value=zoomstop – stop zoon

http://192.168.54.1/cam.cgi?mode=startstream&value=49473 – start video stream on the specified port
http://192.168.54.1/cam.cgi?mode=stopstream


