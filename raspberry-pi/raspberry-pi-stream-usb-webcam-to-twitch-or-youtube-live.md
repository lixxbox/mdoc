---
description: using raspberry pi h264 hardware encoding with ffmpeg.
---

# Stream USB-Webcam to Twitch or Youtube live

##  Compile ffmpeg with h.264 hardware encoder

Clone and compile ffmpeg:

```bash
$ cd /home/pi/
$ sudo apt-get install libomxil-bellagio-dev -y
$ git clone https://github.com/FFmpeg/FFmpeg.git
$ cd FFmpeg
$ sudo ./configure --arch=armel --target-os=linux --enable-gpl --enable-omx --enable-omx-rpi --enable-nonfree

$ sudo make -j4
```

Check if the OpenMAX encoder is present:

```bash
$ ./ffmpeg -encoders | grep h264_omx
```

You should get something like this:

```bash
V..... h264_omx             OpenMAX IL H.264 video encoder (codec h264)
```

Install ffmpeg into your system:

```bash
$ sudo make install
```

## Account preparation

{% tabs %}
{% tab title="Twitch" %}
Go to your twitch channel settings [https://dashboard.twitch.tv/settings/channel](https://dashboard.twitch.tv/settings/channel)

* copy your **private** stream-key
* check low latency mode

Get a recommended ingest endpoint for your area: [https://stream.twitch.tv/ingests/](https://stream.twitch.tv/ingests/)
{% endtab %}

{% tab title="Youtube" %}
Noch nix.

[https://www.youtube.com/live\_dashboard?nv=1](https://www.youtube.com/live_dashboard?nv=1)

[rtmp://a.rtmp.youtube.com/live2](rtmp://a.rtmp.youtube.com/live2)/your\_private\_stream-key
{% endtab %}
{% endtabs %}

## FFmpeg

### Test stream

{% tabs %}
{% tab title="Twitch" %}
Test if your Twitch stream is working, replace **your\_private\_stream-key**:

```bash
$ ffmpeg -f v4l2 -i /dev/video0 -c:v h264_omx -threads 0 -an -f flv "rtmp://live.twitch.tv/app/your_private_stream-key"
```

Check your Twitch channel: [https://www.twitch.tv/**your\_username**](https://www.twitch.tv/your_username)\*\*\*\*
{% endtab %}

{% tab title="Youtube" %}
Noch nix.

Test if your Youtube stream is working, replace **your\_private\_stream-key**:

```bash
$ ffmpeg -f v4l2 -i /dev/video0 -c:v h264_omx -threads 0 -an -f flv "rtmp://a.rtmp.youtube.com/live2
/your_private_stream-key"
```

Check your Youtube channel: **URL**
{% endtab %}
{% endtabs %}

### Streaming settings

In the following step you get a list of supported source video formats. 

Input formats \(e.g. MJPEG, YUYV, ..\), resolutions and framerates

```bash
$ v4l2-ctl --list-formats-ext
```

Transfer the appropriate settings to the following commands:

{% tabs %}
{% tab title="Twitch" %}


```bash
$ ffmpeg -f v4l2 -s 800x600 -r 20 -i /dev/video0 -c:v h264_omx -threads 0 -an -b:v 5M -f flv "rtmp://live-fra05.twitch.tv/app/your_private_stream-key"
```
{% endtab %}

{% tab title="Youtube" %}

{% endtab %}
{% endtabs %}

* Input:

  * -f v4l2  
    * video4linux2
  * ~~-input\_format mjpeg~~
    * ~~format **mjpeg**~~
  * -s 800x600
    * **resolution**
  * -r 20
    * **framerate**
  * -i /dev/video0
    * videoinput -&gt; usb-webcam

* Output:
  * -c:v h264\_omx
    * h.264 hardware encoder
  * -threads 0
    * 0 cpu threads
  * -an
    * no audio
  * -b:v **2M**
    * bitrate, does this have any effect?
  * -f flv "rtmp://live.twitch.tv/app/**your\_private\_stream-key**"
    * twitch url -&gt; ingest endpoint + your\_private\_stream-key

## Autostart......

## Add stream to ..

### .. DWC2

Go to Settings &gt; General &gt; Webcam

* Enter your Webcam-URL [https://player.twitch.tv/?channel=**your\_username**](https://player.twitch.tv/?channel=your_username)\*\*\*\*
* Check "Embed webcam image in an iframe"

### .. Octoprint

so ähnlich, oder über ein plugin :D

