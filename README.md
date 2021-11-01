# BlazorVideoApp
Blazor app that plays a video from a webcam or link (RTSP).

It uses **OpenCV** ([cv::VideoCapture::VideoCapture](https://docs.opencv.org/4.5.3/d8/dfe/classcv_1_1VideoCapture.html)) to capture image from RTSP/Webcam, reads each frame, convert it to a base64 string and puts into a HTML tag **img**.


```
@page "/video"

@using OpenCvSharp;


<img src="@_imgSrc" alt="@_mensagemErro" width="400" height="400"/>

@code {
    private string _imgSrc;
    private string _mensagemErro;

    protected override async Task OnInitializedAsync()
    {
        using (var capture = new VideoCapture("rtsp://wowzaec2demo.streamlock.net/vod/mp4:BigBuckBunny_115k.mov"))

        using (var frame = new Mat())
        {
            try
            {
                while (true)
                {
                    capture.Read(frame);

                    var base64 = Convert.ToBase64String(frame.ToBytes());
                    _imgSrc = $"data:image/gif;base64,{base64}";

                    await Task.Delay(1);

                    StateHasChanged();
                }
            }
            catch (Exception ex)
            {
                _mensagemErro = ex.Message;
            }

        }
    }
}
```
