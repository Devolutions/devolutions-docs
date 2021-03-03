---
uid: wayk-agent-performance
---

# Wayk Agent Performance

## Performance Metrics

The performance of the peer-to-peer connection to the Wayk Agent is largely driven by two factors: capture performance (the speed that updates can be captured), and network speed (the speed that updates can be delivered).

 ### Capture Performance

On Windows 8 and newer, the screen is captured using hardware accelerated DirectX. This is at least 4-5x faster than the fallback software screen capture (GDI). It's possible to disable hardware accelerated captured by setting `DXGICaptureEnabled` to `false` (see [Configuration]('configuration.md')).

Only the updated portions of the screen are transmitted to the client, and only a single display is transmitted at one time.

Capture performance can be affected by the connecting client; see [Client Performance](../client/performance.md).

### Network Performance

Network performance depends greatly on workload and the number of full-screen updates that must be transmitted. Watching a full-screen video generates far more data than interacting with a terminal or file browsing. The following recommendations are based on JPEG/Low quality and are a guideline only.

| Agent Screen Resolution | Size of full screen update (JPEG/Low) | Recommended upstream bandwidth |
| :---------------------: | :------------------------: | :----------------------------: |
| 640x480 (480p) | 30KB | 1Mbps |
| 1280x720 (720p) | 95KB | 3Mbps |
| 1440x900 | 135KB | 5Mbps |
| 1920x1080 | 210KB | 10Mbps |
| 3840x2160 (2160p) | 850KB | 25Mbps |

### Performance Tuning

To achive acceptable performance, make sure you choose a screen resolution that is achievable with the available bandwidth and configure the client performance settings according to recommendations. When using RDP virtual sessions, it's possible for the connecting client to request a specific screen resolution. See  [Client Performance](../client/performance.md).

If the amount of data transmitted by the Agent is too high for the available bandwidth, the connection may be saturated and become laggy. The Agent will transmit frames as fast as it can capture them (which typically might be 8-15fps on modern hardware; or even higher at low resolutions). In this case, the connecting client can request a lower framerate from the Agent. See [Client Performance](../client/performance.md). Start at 6fps and work down to 1fps until you find an acceptable compromise.