# reefminder-pi
Python scripts for ReefMinder modules

Installation of the Camera Module and Installing Streaming Media Server

Install the Raspberry Pi Camera module by inserting the cable into the Raspberry Pi. The cable slots into the connector situated between the Ethernet and HDMI ports, with the silver connectors facing the HDMI port.

Boot up your Raspberry Pi.

From the prompt, run "sudo raspi-config". If the "camera" option is not listed, you will need to run a few commands to update your Raspberry Pi. Run "sudo apt-get update" and "sudo apt-get upgrade"

Run "sudo raspi-config" again - you should now see the "camera" option.

Navigate to the "camera" option, and enable it. Select “Finish” and reboot your Raspberry Pi.


To install the uv4l driver, open the terminal and run the following commands:

$ wget http://www.linux-projects.org/listing/uv4l_repo/lrkey.asc && sudo apt-key add ./lrkey.asc

Add the following line to the file /etc/apt/sources.list :

$ sudo nano /etc/apt/sources.list

deb http://www.linux-projects.org/listing/uv4l_repo/raspbian/ wheezy main

$ sudo apt-get update

$ sudo apt-get upgrade

$ sudo apt-get install uv4l uv4l-raspicam

$ sudo apt-get install uv4l-raspicam-extras

$ sudo apt-get install uv4l-server

$ sudo apt-get install uv4l-uvc

$ sudo apt-get install uv4l-xscreen

$ sudo apt-get install uv4l-mjpegstream

$ sudo reboot

Now start the streaming server

Open the terminal and run the following commands:

$sudo pkill uv4l (Optional)

$sudo uv4l -nopreview --auto-video_nr --driver raspicam --encoding mjpeg --width 640 --height 480 --framerate 20 --server-option '--port=9090' --server-option '--max-queued-connections=30' --server-option '--max-streams=25' --server-option '--max-threads=29'

Notes:

The --port=9090 is the local IP port. You can use any port you like.

The --max-streams=25 is the maximum simultaneous streams.

Finally port forward to your pi static IP and the designated port number.

Access 192.168.1.74:9090/stream