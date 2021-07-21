# Twitch to Youtube

## Functionality

1 - Insert the youtube api provides to you ( studio.youtube.com)
2 - Insert Twitch URL ( Last broadcast or a clip )
3 - Insert Youtube Video title
4 - Starting twitch downloading video process
5 - Take downloaded video and put on Newvideo folderwith the Stating video
6 - Merge the videos
7 - Take output.mp4 and input to youtube

## File Structure


## Twitchtoyt.py

from moviepy.editor import *
import os
from natsort import natsorted
from simple_youtube_api.Channel import Channel
from simple_youtube_api.LocalVideo import LocalVideo

url = input('Twitch url video: ')
title = input('Youtube video title: ')

os.system('cd C:\Users\manuel\Desktop\TwitchtoYoutube\Newvideo &&
twitch-dl download ' + url)

L =[]

for root, dirs, files in
os.walk("C:\Users\manuel\Desktop\TwitchtoYoutube\Newvideo"):

```
#files.sort()
files = natsorted(files)
for file in files:
if os.path.splitext(file)[ 1 ] == '.mp4':
filePath = os.path.join(root, file)
video= VideoFileClip(filePath)
L.append(video)
```
final_clip = concatenate_videoclips(L)
final_clip.to_videofile("output.mp4", fps= 60 , remove_temp=False)

# loggin into the channel
channel = Channel()
channel.login("C:\Users\manuel\Desktop\TwitchtoYoutube\client_secret.json"
, "C:\Users\manuel\Desktop\TwitchtoYoutube\credentials.storage") # For
more information check studio.youtube.com


# setting up the video that is going to be uploaded
video = LocalVideo(file_path="output.mp4")

# setting snippet
video.set_title(title)
video.set_description("")
video.set_tags(["#UrbanroostersNetwork"])
video.set_category("music")
video.set_default_language("es-es")

# setting status
video.set_embeddable(True)
video.set_license("creativeCommon")
video.set_privacy_status("private")
video.set_public_stats_viewable(True)

# setting thumbnail
video.set_thumbnail_path('C:\Users\manuel\Desktop\TwitchtoYoutube\Miniatur
e\miniature.png')

# uploading video and printing the results
video = channel.upload_video(video)
print(video.id)
print(video)

‘

## Example of a real result

https://www.youtube.com/watch?v=K9E8esz3spg&t=1s


