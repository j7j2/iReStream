# iReStream
ReStream RTMP source to any social media.

This small program is designed to grab rtmp content from a computer and allow multiple friends to re-stream the same content on multiple social media account without using paid re-stream services.

Basic usage example.
1- use OBS and configure streaming output to rtmp://127.0.0.1:1935/live/ with streamkey "livestream".

2- get yourself nginx and use the configuration as described below

#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}

rtmp {
        server {
                listen 1935;
				buflen 20s;
                chunk_size 4096;

                application live {
					live on;
					record off;
					
					
                }
        }
}

3- Open the 1935 TCP port in your router to your OBS/nginx machine IP Adress

4- Start the nginx server ( you can monitor it's running in the task manager

5- Start streaming in OBS. Indicator should turn green despite you're not giving anything yet to any social media services. You're only streaming to your local nging server.

6- Have a friend to run iReStream on their pc. In the source box, have them enter rtmp://YourIpAdress/live/livestream  You can also use a DynDns service so that the adress you give your friends don't change if your dynamic IP does. It will then look like rtmp://mycustomdomain.spdns.org/live/livestream

7- Have your friend press the Test button. If successfull, it means that the tool is now able to connect to your local nginx server.

8- Enter the desired social media rtmp server REMEMBER to put a / at the end of the line otherwise it will not connect.

9- have your friend go to his own social media page, click the go live button and get its stream key. Have it paste it in the appropiate field.

10- Have your friend look up the latency setting on the social media streaming dashboard. You should preferably set it to normal for better stability and picture quality.

11- Click Start Streaming. Your friend should now see your content show up in its social media Producer window and should be able to click "go live.

Your content should now be playing live on your friend social media page.

Use bitrate and encoding settings in obs according to both you and you're friends available bandwidth.

You can feed as many friends as you want simultaneously as long as you got the sufficent bandwidth to do so.

It's preferable to ask your friends to avoid using WiFi for those things. Have yourself and your friends do speedtest.net to help you manage global project bandwidth.

With this basic configuration, all your friends will get the same bitrate and encoding from you. Obs and nginx could also be tweaked to have two resolution / bitrate available for the friends with lower bandwidth.

Enjoy and put the social media in fire!
