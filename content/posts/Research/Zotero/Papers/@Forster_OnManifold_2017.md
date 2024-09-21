---
aliases: ["On-Manifold Preintegration for Real-Time Visual--Inertial Odometry", "Christian Forster, Luca Carlone, Frank Dellaert, Davide Scaramuzza (2017) On-Manifold Preintegration for Real-Time Visual--Inertial Odometry"]
title: "On-Manifold Preintegration for Real-Time Visual--Inertial Odometry"
authors: [Christian Forster, Luca Carlone, Frank Dellaert, Davide Scaramuzza]
---

> [!info]- Metadata
> abstract:: Current approaches for visual–inertial odometry (VIO) are able to attain highly accurate state estimation via nonlinear optimization. However, real-time optimization quickly becomes infeasible as the trajectory grows over time; this problem is further emphasized by the fact that inertial measurements come at high rate, hence, leading to the fast growth of the number of variables in the optimization. In this paper, we address this issue by preintegrating inertial measurements between selected keyframes into single relative motion constraints. Our ﬁrst contribution is a preintegration theory that properly addresses the manifold structure of the rotation group. We formally discuss the generative measurement model as well as the nature of the rotation noise and derive the expression for the maximum a posteriori state estimator. Our theoretical development enables the computation of all necessary Jacobians for the optimization and a posteriori bias correction in analytic form. The second contribution is to show that the preintegrated inertial measurement unit model can be seamlessly integrated into a visual–inertial pipeline under the unifying framework of factor graphs. This enables the application of incremental-smoothing algorithms and the use of a structureless model for visual measurements, which avoids optimizing over the 3-D points, further accelerating the computation. We perform an extensive evaluation of our monocular VIO pipeline on real and simulated datasets. The results conﬁrm that our modeling effort leads to an accurate state estimation in real time, outperforming state-of-the-art approaches.
> pdf:: [Preintegration_240503_121125.pdf](zotero://select/library/items/NHMJU56G)
> bibliography:: "[1]

C. Forster, L. Carlone, F. Dellaert, and D. Scaramuzza, ‘On-Manifold Preintegration for Real-Time Visual--Inertial Odometry’, _IEEE Trans. Robot._, vol. 33, no. 1, pp. 1–21, Feb. 2017, doi: [10.1109/TRO.2016.2597321](https://doi.org/10.1109/TRO.2016.2597321)."


🔥🔥🔥everything above this line might change during an update 🔥🔥🔥
%% begin notes %%
%% end notes %% 
%% begin annotations %%
 
⬇️*Imported (Annotations) on 2024-05-12#23:25:37*⬇️



> [!annotation-yellow] Highlight
>hence, we would have to add new states in the estimation at every new IMU measurement [37].(p. [7](zotero://open-pdf/library/items/NHMJU56G?page=7&annotation=RW5BPVWE))>
> **comment:**
> test
> [[2024-05-12#23:02]]
⬇️*Imported (Annotations) on 2024-05-12#23:52:29*⬇️



> [!annotation-yellow] Image
> ![[Zotero/images/@Forster_OnManifold_2017/image-5-x328-y624.png|300]]
> [[2024-05-12#23:51]]
%% end annotations %%

%% Import Date: 2024-05-12T23:52:33.662+09:00 %%
