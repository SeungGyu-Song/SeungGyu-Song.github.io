---
aliases: 
date: 
title: 
URL: 
tags: 
draft: true
---
### Objective
- [[🧩OpenVINS Code Analysis|OpenVINS]]에서 소개된 Zero Velocity Update (ZUPT)를 이해해보자!

### Future Work
- 내가 이해 못한 부분을 어떻게 보완할 수 있을까?

### Part 1
Monocular system에서 temporal SLAM feature가 없을 때 중요하게 작동할 수 있다.
로봇이 가만히 있으면 triangulation도 안 되고, 이에 따라 Update를 할 수가 없게 됨. 
→ Stereo cam 사용 or temporal SLAM feature를 확보하기

추가적으로 Stereo나 temporal SLAM이 있더라도 dynamic한 object들에 대해서는 대처방안이 없다. 하지만, ZUPT를 통해서 이에 대응할 수 있따. 

### Part 2


### ❓️Questions

