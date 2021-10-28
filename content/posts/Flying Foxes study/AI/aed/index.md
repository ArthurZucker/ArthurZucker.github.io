---
title: "PAMAI : Audio Event Detection"
date: 2021-10-18
description: In this part I will explain our research in Audio Event Detection. 
menu:
  sidebar:
    name:  Audio Event Detection
    identifier: pamai-ai-aed
    weight: 10
    parent: pamai-ai
hero: pipeline2.png
draft: false
---

My most recent results are available! I implemented the SincNet in Pytorch! My results were logged using [](wandb), an amazing visualisation tool for sweeps. The dataset is, for now, a third of the Egyptian FruitBat dataset. Soon, I will add other animal recordings in order to asset the generalisation performances of my network! 

I will also compute the IoU for the best classes, and shall compare this implementation with my trainings on YOLOR (You Only Learn One Reprensentation) which I previously implemented. 

I look forward to sharing more. My next task will be to implementd DENet, which is only available on tensorflow, and integrate transformers to my architectures. 