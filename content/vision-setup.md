---
title: "Setting up and Tuning Vision"
---

### Overview

Vision before you can even get your hands dirty requires some setting up and adjusting for the best processing that is crucial for in game performance. Vision can be applied through different camera processing methods such as PhotonVision and Limelight. The [PhotonVision](https://docs.photonvision.org/en/v2026.1.1/) and [Limelight](https://docs.limelightvision.io/docs/docs-limelight/getting-started/summary) docs can be found through these two links.These docs contain what you need to setup the different cameras and ability to have successful vision processing and tracking.

### Requirements

Things you SHOULD have with you at hand when doing any calibration activity:

-[limelight.local](limelight.local) (Website to connect to Limelight pipeline) -[photonvision.local](photonvision.local:5800) (Website to connect to Photonvision pipeline)

- Both of the documents on hand to help with setup
- Charuco Calibration Board

### General Process

Obviously, the documents provide the knowledge you need for both code and physical setup to your computer, but after you get whatever camera setup, you need be able to calibrate and tune the camera vision under different conditions. This is due to the fact that when we go to any competition, we have to calibrate the cameras to the field itself as lighting varies in different rooms. Here are the steps you must follow:

- Firstly, get a Charuco Calibration Board, as this is what you will position in front of your camera and this will allow for the camera to be calibrated to accurately process the game objects and field. The Charuco board is found in the shop, and we make sure that the picture of the Charuco image itself is plastered on the cardboard piece as flat as possible to avoid variations.
- Next, access the pipeline of whatever you are using, this will provide different sliders to adjust lighting, color contrast (Red and Blue Balance Specifically), and sensor grain. There is no formula to adjust these to properly calibrate the camera, you have to play around and make sure the camera senses every part of the board fully as it will highlight the parts it detects.
- Finally, once you play around and get the board fully highlighted, then the camera is ready for tracking and detecting objects on the field.

![limelight](/limelight-pipeline.png) ![charucoboard](/charucoboard.png)
