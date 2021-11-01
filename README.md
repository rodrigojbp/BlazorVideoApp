# BlazorVideoApp
Blazor app that plays a video from a webcam or link (RTSP).

It uses OpenCV (cv::VideoCapture::VideoCapture) to capture image from RTSP/Webcam, reads each frame, convert it to a base64 string and puts into a HTML img.
