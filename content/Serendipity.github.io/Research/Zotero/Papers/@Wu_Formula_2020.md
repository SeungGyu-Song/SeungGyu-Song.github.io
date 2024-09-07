---
aliases: ["Formula Derivation and Analysis of the VINS-Mono", "Yibin Wu (2020) Formula Derivation and Analysis of the VINS-Mono"]
title: "Formula Derivation and Analysis of the VINS-Mono"
authors: [Yibin Wu]
---


#zotero/🏃‍ #zotero/computer_science_-_computer_vision_and_pattern_recognition  #zotero/computer_science_-_robotics  

> [!info]- Metadata
> abstract:: The VINS-Mono is a monocular visual-inertial 6 DOF state estimator proposed by Aerial Robotics Group of HKUST in 2017. It can be performed on MAVs, smartphones and many other intelligent platforms. Because of the excellent robustness, accuracy and scalability, it has gained extensive attention worldwide. In this manuscript, the main equations including IMU pre-integration, visual-inertial co-initialization and tightly-coupled nonlinear optimization are derived and analyzed.
> pdf:: [Wu_2020_Formula Derivation and Analysis of the VINS-Mono.pdf](zotero://select/library/items/GJNP7AZ3)
> extra:: "arXiv:1912.11986 [cs]"
> bibliography:: "[1]

Y. Wu, “Formula Derivation and Analysis of the VINS-Mono.” arXiv, Sep. 19, 2020. doi: [10.48550/arXiv.1912.11986](https://doi.org/10.48550/arXiv.1912.11986)."


🔥🔥🔥everything above this line might change during an update 🔥🔥🔥
%% begin notes %%
%% end notes %% 
%% begin annotations %%
 ⬇️*Imported (Annotations) on 2024-05-13#22:39:51*⬇️



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-12-x135-y461.png|300]]
> [[2024-05-13#21:55]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-12-x180-y360.png|300]]
> [[2024-05-13#21:55]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-12-x163-y201.png|300]]
> [[2024-05-13#21:56]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-12-x142-y99.png|300]]
> [[2024-05-13#21:56]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-13-x129-y410.png|300]]
> [[2024-05-13#21:57]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-13-x194-y347.png|300]]
> [[2024-05-13#21:57]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-13-x126-y142.png|300]]
> [[2024-05-13#21:58]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-13-x133-y87.png|450]]
> [[2024-05-13#21:58]]



> [!annotation-yellow] Highlight
>We calculate the increment of attitude in (3) so , then we update the states by the quaternion of the attitude increment. This is implemented by instantiating “LocalParameterization” in ceres solver [14].(p. [14](zotero://open-pdf/library/items/GJNP7AZ3?page=14&annotation=ZPS5P9VF))>
> **comment:**
> 최적화 후 quaternion을 update하는 방법.
> [[2024-05-13#21:59]]


quaternion variable 
> [!annotation-yellow] Quaternion Variable
>Therefore, the dimensions of the Jacobian matrix in the IMU residual model should be <15×7, 15×9, 15×7, 15×9>. Therefore the last row of   0 J and   2 J is zero.(p. [14](zotero://open-pdf/library/items/GJNP7AZ3?page=14&annotation=LGT972ZR))>
> **comment:**
> quaternion은 변수 4개이고, 실제 rotation의 변수인 3개보다 많아서 overparameterization이 되므로 마지막이 0이 됨. -> 실제 코드에서 어떻게 활용됐는지 체크하기
> [[2024-05-13#22:01]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-16-x203-y441.png|300]]>
> **comment:**
> Vision 모델 state
> [[2024-05-13#22:03]]
⬇️*Imported (Annotations) on 2024-05-15#16:14:16*⬇️



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-3-x184-y100.png|300]]
> [[2024-05-15#16:13]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Wu_Formula_2020/image-6-x203-y67.png|300]]
> [[2024-05-15#16:13]]



> [!annotation-yellow] Highlight
>We assume the uncertainty of measurement is Gaussian distributed, namely, ( , ) z NzQ .(p. [12](zotero://open-pdf/library/items/GJNP7AZ3?page=12&annotation=N3AM6YV5))
> [[2024-05-13#22:49]]
%% end annotations %%

%% Import Date: 2024-05-15T16:14:22.453+09:00 %%
