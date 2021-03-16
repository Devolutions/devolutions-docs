---
uid: wayk-client-performance
---

# Wayk Client Performance

## Performance Options

Several options are available that affect the performance and experience of the connection.

![Wayk Client - Performance](../../images/wayk_client_performance.png)

| Setting       | Description |
|:------------- |:----------- |
| Quality mode | Low, medium (default) or high. Higher quality provides a better image quality, but performance will be worse. |
| Preferred codec | The codec to use for image compression. JPEG and GFWX are tuned to provide similar performance characteristics at the equivalent quality modes. |
| Display deskop wallpaper | Disable to replace desktop wallpaper on the Agent with a blank background. Windows Agents only. |
| Show window contents when dragging | Disable to prevent window contents from being rendered during drag operations. Windows Agents only. |
| Animate menus | Disable to turn off animation effects on menus. Windows Agents only. |

Further performance options are available. These can be configured using the [Command Line](configuration.md).

| Setting Name | Description | Values |
| :----------- | :---------- | -----: |
| MaxFrameRate | The maximum number of frames per second for the Agent to try and transmit | Frames per second from '1' to '30' (*default*) |
| DesktopWidth | When using RDP virtual sessions, the requested width of the remote display. '0' accepts the default value from the Agent. | Width in pixels from '0' (*default*) to '3840' |
| DesktopHeight | When using RDP virtual sessions, the requested height of the remote display. '0' accepts the default value from the Agent. | Height in pixels from '0' (*default*) to '2160' |
| ScalingMode | Choose the scaling (if any) performed by the Agent on the desktop image. Windows Agents only. | See [Scaling Mode](#scaling-mode) |

### Scaling Mode

Possible values are:

**0** Automatic (*Default*). The image is scaled (or not) depending on the display resolution of the Agent.

**1** Scaled. The image is scaled to the perceived display resolution of the Agent.

**2** Full. The image is the full display resolution of the Agent.


## Recommended Settings

For optimum performance, configure "Low" or "Medium" quality modes and disable all the "Experience" effects (desktop background, show window contents when dragging, and animate menus). Ensure that "ScalingMode" is set to "Automatic" or "Scaled". If using RDP virtual sessions, select a low display resolution.