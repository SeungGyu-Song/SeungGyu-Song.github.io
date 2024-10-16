내 생각에는 다른 거 같다.

[[📦️Error-state Kalman Filter]]를 보면 jacobian 을 구할 때
$$\frac{\partial{L}}{\partial{p}} * \frac{\partial{p}}{\partial \delta p}$$
가 되어야 하는데, 즉, 미소 변화량 $\delta p$에 대해서도 미분을 해준 값이 들어가야하는데 그렇지 않다.

[[🧩VINS-Fusion Map.canvas|🧩VINS-Fusion Map]]은 그냥 $\frac{\partial L}{\partial p}$에서 끝나는 거 같다.