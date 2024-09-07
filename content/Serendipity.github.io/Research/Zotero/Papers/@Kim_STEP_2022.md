---
aliases:
  - "STEP: State Estimator for Legged Robots Using a Preintegrated Foot Velocity Factor"
title: "STEP: State Estimator for Legged Robots Using a Preintegrated Foot Velocity Factor"
authors:
  - Yeeun Kim
  - Byeongho Yu
  - Eungchang Mason Lee
  - Joon-ha Kim
  - Hae-won Park
  - Hyun Myung
---


> [!info]- Metadata
> abstract:: We propose a novel state estimator for legged robots, STEP, achieved through a novel preintegrated foot velocity factor. In the preintegrated foot velocity factor, the usual non-slip assumption is not adopted. Instead, the end effector velocity becomes observable by exploiting the body speed obtained from a stereo camera. In other words, the preintegrated end effector’s pose can be estimated. Another advantage of our approach is that it eliminates the necessity for a contact detection step, unlike the typical approaches. The proposed method has also been validated in harsh-environment simulations and real-world experiments containing uneven or slippery terrains.
> pdf:: [STEP_State_Estimator_for_Legged_Robots_Using_a_Preintegrated_Foot_Velocity_Factor.pdf](zotero://select/library/items/V2M9YNV7)
> bibliography:: "[1]

Y. Kim, B. Yu, E. M. Lee, J. Kim, H. Park, and H. Myung, “STEP: State Estimator for Legged Robots Using a Preintegrated Foot Velocity Factor,” _IEEE Robot. Autom. Lett._, vol. 7, no. 2, pp. 4456–4463, Apr. 2022, doi: [10.1109/LRA.2022.3150844](https://doi.org/10.1109/LRA.2022.3150844)."


🔥🔥🔥everything above this line might change during an update 🔥🔥🔥
%% begin notes %%
%% end notes %% 
%% begin annotations %%
 
 
⬇️*Imported (Annotations) on 2024-05-20#23:00:04*⬇️



> [!annotation-red] Highlight
>Even though previous studies assumed the slip effect could be modeled as Gaussian noise (or bias), this approach might be invalid under severe slip.(p. [2](zotero://open-pdf/library/items/V2M9YNV7?page=2&annotation=T3DR88EJ))>
> **comment:**
> 왜? slip이 많이 일어나는 값은 분포의 양 끝으로 확률값이 적어져서?
> [[2024-05-20#22:18]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Kim_STEP_2022/image-3-x87-y72.png|300]]
> [[2024-05-20#22:23]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Kim_STEP_2022/image-4-x51-y619.png|300]]
> [[2024-05-20#22:27]]



> [!annotation-yellow] Highlight
>When  ̃ α(t) is given, by using the leg kinematics model, the foot position s(t) ∈ R3 and orientation Ψ(t) ∈ SO(3) in the world frame(p. [4](zotero://open-pdf/library/items/V2M9YNV7?page=4&annotation=NA7X7LTG))
> [[2024-05-20#22:28]]



> [!annotation-yellow] Highlight
>bΓp(·) and bΓR(·) are the end effector position and orientation(p. [4](zotero://open-pdf/library/items/V2M9YNV7?page=4&annotation=L6JFNRKE))
> [[2024-05-20#22:28]]



> [!annotation-yellow] Highlight
>calculated by forward kinematics(p. [4](zotero://open-pdf/library/items/V2M9YNV7?page=4&annotation=CE4UG3EI))
> [[2024-05-20#22:28]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Kim_STEP_2022/image-5-x92-y441.png|300]]
> [[2024-05-20#22:55]]



> [!annotation-yellow] Highlight
>Note that (27) should be transformed to the foot frame and expressed with sensor measurements to find the preintegrated foot measurement. We manipulate (27) by multiplying Ψ  to both sides and augmenting the measurements(p. [5](zotero://open-pdf/library/items/V2M9YNV7?page=5&annotation=Y7FSG62W))
> [[2024-05-20#22:56]]



> [!annotation-red] Highlight
>(24) can be discretized based on the assumption that f  ̃ ω is constant during sampling time Δt:(p. [5](zotero://open-pdf/library/items/V2M9YNV7?page=5&annotation=MS9XXLBT))>
> **comment:**
> 실제로 foot angular velocity는 등속도가 아닐 수 있으니까 여기서 오차가 쌓일 수 있음.
> [[2024-05-20#22:57]]

^344201



> [!annotation-red] Highlight
>Here, we assume that the body velocity used in (28) between i and j is constant.(p. [5](zotero://open-pdf/library/items/V2M9YNV7?page=5&annotation=WC72CRSS))
> [[2024-05-20#22:58]]

^3f6575



> [!annotation-yellow] Highlight
>To avoid dependency on foot position si,(p. [5](zotero://open-pdf/library/items/V2M9YNV7?page=5&annotation=NH6C7YJS))
> [[2024-05-20#22:58]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Kim_STEP_2022/image-6-x51-y496.png|300]]
> [[2024-05-20#22:58]]



> [!annotation-yellow] Image
> ![[Zotero/images/@Kim_STEP_2022/image-6-x55-y335.png|300]]
> [[2024-05-20#22:58]]
%% end annotations %%

%% Import Date: 2024-05-20T23:00:08.967+09:00 %%
