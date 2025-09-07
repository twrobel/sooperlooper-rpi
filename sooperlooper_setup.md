Optional set mic gain

amixer -D hw:2 sset 'Mic' 70%

Start jack
jackd -d alsa -d hw:2,0 -r 44100 -p 512 -n 3

Start sooperlooper
sooperlooper -S default

tomas@raspberrypi:~ $ jack_lsp
system:capture_1
system:playback_1
system:playback_2

Connect things
jack_connect system:capture_1 system:playback_2 & \
jack_connect system:capture_1 sooperlooper:common_in_1 & \
jack_connect system:capture_1 sooperlooper:common_in_2 & \
jack_connect sooperlooper:common_out_1 system:playback_2 & \
jack_connect sooperlooper:common_out_2 system:playback_2

slgui -S default -J sooperlooper -P 9952

oscsend osc.udp://raspberrypi:9952/ /sl/0/hit s record
