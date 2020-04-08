# [squeezelite](https://sourceforge.net/projects/lmsclients/files/squeezelite/linux/)

Purpose
--
Headless player to be used with Logitech Squeezebox server.

Configuration
--
Config-File: /usr/local/bin/squeezelite.sh

Options: Define MAC-address, player name, server IP, port, soundcard, etc. 
Also see: [Manual](http://manpages.ubuntu.com/manpages/trusty/man1/squeezelite.1.html)

Example:
~~~
SL_NAME="Player"
SB_SERVER_CLI_PORT="9090"
SL_SOUNDCARD="plughw:CARD=ALSA"
SB_SERVER_IP="10.0.0.100"
SL_USER="smarthome"
ALSABUFFER=320
PERIODS=4
BIT=16
MMAP=0
SL_ALSA_PARAMS="$ALSABUFFER:$PERIODS:$BIT:$MMAP"
STREAMINGBUFFERIN=2048
STREAMINGBUFFEROUT=2048
STREAMINGBUFFER="$STREAMINGBUFFERIN:$STREAMINGBUFFEROUT"
MAXSAMPLERATE=48000
PRIORITY=90
SL_ADDITIONAL_OPTIONS="-b ${STREAMINGBUFFER} -r ${MAXSAMPLERATE} -p ${PRIORITY}"
SB_SERVER_IP="10.0.0.100"
SL_USER="smarthome"
~~~


Restart **systemctl restart squeezelite**
