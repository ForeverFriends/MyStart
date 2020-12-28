```mermaid
classDiagram

class Camera
Camera: -CameraBuffer* m_Buffer
Camera: -CameraSrc* m_CamerSrc
Camera: -CameraRtspServer* m_RtspServer
Camera: +Camera()
Camera: +Camera(CameraType type, QSize pictureSize)
Camera: +buffer()
Camera: +capture() virtual QString =0
Camera: +startRecord() virtual viod =0 
Camera: +stopRecord() virtual viod =0

Camera <|-- PalCamera
Camera <|-- FpdLinkCamera
Camera *-- CameraBuffer
Camera *-- CameraSrc
Camera *-- CameraRtspServer

PalCamera: -CameraCapture* m_pCapture
PalCamera: -CameraRecord* m_pRecord
PalCamera: +PalCamera(CameraType type, QSize palSize)
PalCamera: +capture() virtual QString
PalCamera: +startRecord() virtual void
PalCamera: +stopRecord() virtual void

PalCamera *-- CameraCapture
PalCamera *-- CameraRecord

FpdLinkCamera: -CameraCapture* m_pCapture
FpdLinkCamera: -CameraRecord* m_pRecord
FpdLinkCamera: +PalCamera(CameraType type, QSize palSize)
FpdLinkCamera: +capture() virtual QString
FpdLinkCamera: +startRecord() virtual void
FpdLinkCamera: +stopRecord() virtual void

FpdLinkCamera *-- CameraCapture
FpdLinkCamera *-- CameraRecord


CameraCapture: -CustomData* m_pData
CameraCapture: -QMutex m_mutex
CameraCapture: -CameraBuffer* m_pBuffer
CameraCapture: CameraCapture(CameraBuffer* buffer,  QSize size)
CameraCapture: -gstInit() virtual void
CameraCapture: +capture() QString
CameraCapture: +cb_need_data(GstElement* element, guint unused_size, gpointer user_data) static void
CameraCapture: +cb_message(GstBus* bus, GstMessage* msg, gpointer user_data) static void

CameraCapture o--CameraBuffer

CameraRecord: -CustomData* m_pData
CameraRecord: -CameraBuffer* m_pBuffer
CameraRecord: -QMutex m_mutex
CameraRecord: -bool m_bRecording
CameraRecord: +CameraRecord(CameraBuffer* buffer,  int width, int height)
CameraRecord: -gstInit() virtual void
CameraRecord: -gstFinalize() virtual void
CameraRecord: +cb_need_data(GstElement *element, guint unused_size, gpointer user_data) static void
CameraRecord: +cb_message (GstBus *bus, GstMessage *msg, gpointer user_data) static void
CameraRecord: +startRecord() virtual void
CameraRecord: +stopRecord() virtual void

CameraRecord o--CameraBuffer

CameraBuffer: -uint m_nSize
CameraBuffer: -void* m_buffer
CameraBuffer: -QReadWriteLock* m_rwLock
CameraBuffer: +buffer() void*
CameraBuffer: +readBuffer(void* bf) void
CameraBuffer: +writeBuffer(void* bt, int size) void

CameraSrc: -CameraControlListener m_Listener
CameraSrc: -CameraControl*  m_control
CameraSrc:  +on_data_raw_image_cb(void *data, int size, void *userData) static void
CameraSrc:  +startPreview()	
CameraSrc:  +stop()






```

```mermaid
classDiagram
calss CameraBase


```









## gst-rtsp-server 编译依赖

下载地址：http://repo2.insyber.com/syberos:/os2.1_tyw_1881:/base/standard_armv7tnhl/armv7tnhl/

- meson
  1. ​	ninja
  2. python3-setuptools
- gettext
  1. ​	gettext-devel
     1. cvs
        1. nano
     2. gettext-libs
- gst-plugins-bad
  - orc-devel
- gst-plugins-bad-devel







## gst --Test

- ./test-launch  "( videotestsrc pattern=1 ! avenc_h263 ! rtph263pay name=pay0 pt=96 )"
- ./test-launch  "( videotestsrc pattern=18 ! videoconvert ! omx_h264enc ! h264parse ! rtph264pay name=pay0 pt=96 )"
- ./test-launch  "( videotestsrc pattern=18 ! capsfilter caps="video/x-raw,width=1280,height=720" ! omx_h265enc ! rtph265pay name=pay0 pt=96 )"
- gst-inspect-1.0 playbin uri=rtsp://192.168.42.1:8554/test
- gst-inspect-1.0 | grep pay
- gst-launch-1.0 -e rtspsrc location=rtsp://192.168.42.1:8554/test ! rtph265depay ! filesink location=./test.h265
- ./test-launch  "( videotestsrc pattern=18 ! capsfilter caps="video/x-raw,width=1280,height=720" ! omx_h265enc ! rtph265pay name=pay0 pt=96 )"







## mjpeg dec

1、原Pipe拼装

```mermaid
graph LR
appsrc --> jpegdec --> ffmpegcolorspace --> appsink
```

