# jetson-gstreamer

Full details [here](https://docs.nvidia.com/jetson/l4t/index.html#page/Tegra%20Linux%20Driver%20Package%20Development%20Guide/accelerated_gstreamer.html#wwpID0E02P0HA)

Play from USB cam:
```
gst-launch-1.0 v4l2src device="/dev/video0" ! "video/x-raw, format=(string)YUY2" ! xvimagesink -e
gst-launch-1.0 v4l2src device="/dev/video0" ! "video/x-raw, width=640, height=480, format=(string)YUY2" ! xvimagesink -e

```

To play a video:
```
gst-launch-1.0 filesrc location=video.mp4 ! qtdemux name=demux ! h264parse ! omxh264dec ! nvoverlaysink -e


```