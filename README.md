# ffmepg
ffmpeg settings for various things


<h4>Here for install instuctions:</h4>
https://trac.ffmpeg.org/wiki/CompilationGuide/MacOSX

From the CLI:
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

From the CLI:
brew install ffmpeg



<h4>Mp4 with bit rate and fixed dimensions:</h4>

ffmpeg -i video.mp4 -vf scale=640:360 -c:v libx264 -b:v 600K video_640x360_600kbps.mp4

-c:v: Mp4 codec
-b:v: Bitrate


<h4>Jpeg sequence settings:</h4>

ffmpeg -i video.mp4 -vf scale=-1:720 -qscale:v 3 video_%d.jpg

scale: adjusts the aspect ratio to 720p
-qscale: adjust the jpeg quality
%d: outputs digits 



<h4>Trim a video:</h4>

ffmpeg -i video.mp4 -ss 00:00:00 -t 00:00:00 -an video_trimmed.mp4

-ss: start time
-t: length of time to copy from the start time



<h4>Crop a video:</h4>

ffmpeg -i video.mp4 -vf "crop=1280:400:350:300" -ss 00:00:07 -t 00:00:08 -c:v libx264 -preset veryslow -s 1280x400 -q 9 -an video_loop.mp4

-vf "crop=1280:400:350:300": takes a 1280x400 crop starting at 350px from the top, and 300px from the left



<h4>Export a poster image:</h4>
ffmpeg -ss 0 -i video.mp4 -qscale:v 1 -vframes 1 poster.jpg

-ss: The time from which to take the poster
-vframes 1: exports one frame