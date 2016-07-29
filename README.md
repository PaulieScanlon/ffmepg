# ffmepg
ffmpeg settings for various things


Here for install instuctions:
https://trac.ffmpeg.org/wiki/CompilationGuide/MacOSX

From the CLI:
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

From the CLI:
brew install ffmpeg



Mp4 with bit rate and fixed dimensions:

ffmpeg -i video.mp4 -vf scale=640:360 -c:v libx264 -b:v 600K video_640x360_600kbps.mp4

-c:v: Mp4 codec
-b:v: Bitrate


Jpeg sequence settings:

ffmpeg -i video.mp4 -vf scale=-1:720 -qscale:v 3 video_%d.jpg

scale: adjusts the aspect ratio to 720p
-qscale: adjust the jpeg quality
%d: outputs digits 



Trim a video:

ffmpeg -i video.mp4 -ss 00:00:00 -t 00:00:00 -an video_trimmed.mp4

-ss: start time
-t: length of time to copy from the start time



Crop a video:

ffmpeg -i video.mp4 -vf "crop=1280:400:350:300" -ss 00:00:07 -t 00:00:08 -c:v libx264 -preset veryslow -s 1280x400 -q 9 -an video_loop.mp4

-vf "crop=1280:400:350:300": takes a 1280x400 crop starting at 350px from the top, and 300px from the left



Export a poster image:
ffmpeg -ss 0 -i video.mp4 -qscale:v 1 -vframes 1 poster.jpg

-ss: The time from which to take the poster
-vframes 1: exports one frame
