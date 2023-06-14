# First blog of my contributions to QuTiP
Hi. My name is Yuji Tamakoshi. For the next three months, I will be updating my blog with my contributions to the Google Summer of Code (GSoC) project. I hope my blog will be helpful to someone in the near future!

## What is QuTiP?
According to QuTiP website, QuTiP is an open-source software for simulating the dynamics of open quantum systems [1]. If you are interested in QuTiP after reading this blog, please check out the tutorials on the website and try them out on Google Colaboratory. Let's experience the wonders and fascination of quantum systems together!

## Overview of my project
I will be focusing on improving the visualization capabilities of QuTiP. Visualization, such as graphs and animations, often helps people understand things better, and the same applies to understanding quantum mechanics.
The outline of my project is as follows: 
QuTiP already has several visualization functions, but they can sometimes be unfriendly to users due to unchangeable colors and disorganized arguments. This project aims to enhance these functions by unifying their interfaces and adding colorblind options. Additionally, I will develop an animation function for the evolution of quantum states. The final deliverables will include unified interfaces for plot functions with colorblind support, animation functions for the Result object, as well as pytests and documentation for all of these features.
You can find more details about [my project](https://docs.google.com/document/d/1s66NPwtaFdaMp8p8nJi1qxfbzxhZyDW6Z6_aodu4sjw/edit?usp=sharing) here.

## What is next?
Currently, I am working on introducing a new class to make QuTiP more colorblind-friendly, and selecting function arguments to make them more intuitive for beginners. I will write them in my next blog post.

You can follow my current activities through [this link](https://github.com/qutip/qutip/pull/2170), and [PR-2113](https://github.com/qutip/qutip/pull/2113) and [PR-2120](https://github.com/qutip/qutip/pull/2120) are my contributions to QuTiP. If you are interested in contribution. See [this](https://qutip.org/docs/latest/development/contributing.html) and try!

[1] https://qutip.org/
