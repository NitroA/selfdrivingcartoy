<h3 align="center">
  <img src="assets/jetson_icon_web.png" width="300">
</h3>

# Jetson

Jetson is a self-driving toy car project. It contains an end-to-end CNN system build in PyTorch.

Check out corresponding Medium article:

[Jetson - Self-Driving Toy Car (Part: 1)](https://towardsdatascience.com/jetson-self-driving-toy-car-part-1-4341c139c0f2)

<img src="assets/pov.gif">

## Hardware

Any RC Car chasis with controllable throttle (longitude) and steering (lateral) should be compatible. 

There is a bunch options to start with. I recommend checking [nvidia's suggestions](https://github.com/NVIDIA-AI-IOT/jetracer#cars), [donkey car docs](http://docs.donkeycar.com/guide/build_hardware/) or [waveshare AI kit](https://www.waveshare.com/wiki/JetRacer_AI_Kit) which is used in this project.


<img src="assets/assembly.gif">

### Senors
* Front facing wide-angle camera with 160° FOV

### Brain
* Jetson Nano by NVIDIA

## Software

### Prerequisites
* [jetcard](https://github.com/NVIDIA-AI-IOT/jetcard)
* [jetcam](https://github.com/NVIDIA-AI-IOT/jetcam)
* [jetracer](https://github.com/NVIDIA-AI-IOT/jetracer)
* [torch2trt](https://github.com/NVIDIA-AI-IOT/torch2trt)

*when using waveshare's kit, you might need to use waveshare's forks of the above repos, see [link](https://www.waveshare.com/wiki/JetRacer_AI_Kit)

### 1. Data Collection
[Notebook](autopilot_data_collection.ipynb)
<br>
<br>
The main goal of this stage is to gather data reflecting correct driving, i.e images with correctly annotated steering and throttle values.
While driving with gamepad, you can record camera frames and save corresponding steering and throttle values. An example piece of data may look as follows:
<br>
<img src="assets/5178962045858.jpg">
<br>
[0.3, 0.5]

Where the first value is a steering value and the second one is a throttle value. Both of them range from -1.0 to 1.0.

I recommend collecting at least 20k of samples, but usually the more the merrier.

### 2. Training

[Notebook](autopilot_training.ipynb)
<br>
<br>
Training process consists of iterating over previously gathered datasets and feeding them into the CNN. I recommend offloading data from Jetson Nano and performing training on the GPU as the process might be heavy on the resources.

<img src="assets/training_progress.jpg">


### 3. Testing
[Notebook](autopilot_testing.ipynb)
<br>
<br>
Finally, with the trained model we can test our jetson on the track. With relatively lightweight resnet18 CNN, Jetson operates at ~30 FPS and successfully drives the track in both directions. Moreover, it does so without being explicitly instructed to follow lanes. Jetson learned it implicitly with the end-to-end system.

<img src="assets/loop_ccw_small.gif" width=500>
<img src="assets/loop_cw_small.gif" width=500>

## Author

**Greg (Grzegorz) Surma**

[**PORTFOLIO**](https://gsurma.github.io)

[**GITHUB**](https://github.com/gsurma)

[**BLOG**](https://medium.com/@gsurma)

<a href="https://www.paypal.com/paypalme2/grzegorzsurma115">
  <img alt="Support via PayPal" src="https://cdn.rawgit.com/twolfson/paypal-github-button/1.0.0/dist/button.svg"/>
</a>
