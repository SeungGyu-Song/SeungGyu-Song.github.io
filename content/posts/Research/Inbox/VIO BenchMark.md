
| Name                                      | Feature Extractor   | Feature Tracking | Backend         | CPU  |
| ----------------------------------------- | ------------------- | ---------------- | --------------- | ---- |
| [[🧩VINS-Fusion Map.canvas\|VINS-Fusion]] | GoodFeaturestoTrack | OpticalFlowLK    | Optimization    | 270% |
| [[👑BASALT.canvas\|BASALT]]               | FAST                | own-made         | Optimization    | 70%  |
| [[🧩OpenVins.canvas\|OpenVINS]]           | FAST                | OpticalF         | Error-state EKF | 37%  |
|                                           |                     |                  |                 |      |
|                                           |                     |                  |                 |      |
BASALT ros wrapper에 뭐가 문제가 있나봄 (ROS로 돌리면 300% 이렇게 찍히던데)