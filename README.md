# nanoFramework.WS2812
A C# helper class that helps you control pixels on WS2812 addressable RGB devices with the nanoFramework platform and esp32.

This is a wrapper class library that uses the RMT library from this repository --> https://github.com/ololoshka2871/nanoFramework.Hardware.Esp32.RMT

So in order to run the WS2812 library you first need to include the RMT to your image, build it and flash it to your device. That process is explained here --> https://jsimoesblog.wordpress.com/2018/06/19/interop-in-net-nanoframework/
Also here is the exact process and everything you need to build and flash you own image from nf-interop for esp32 --> http://docs.nanoframework.net/content/getting-started-guides/build-esp32.html

Here is an example of code how to make rainbow effect:

```C#
int ledCount = 90;
PixelController controller = new PixelController(18, 10, false);

int step = 360 / ledCount;
var hue = 0;
for (uint i = 0; i < ledCount; i++)
{                
    controller.SetHSVColor((short)i, (short)hue, 1, 0.05f); 
    hue = hue + step;  
    controller.UpdatePixels();
}
for(; ;)
{
    controller.MovePixelsByStep(1);
    controller.UpdatePixels();
    System.Threading.Thread.Sleep(10);
}
```
