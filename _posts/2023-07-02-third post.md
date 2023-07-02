# Continue working on visualization.py
Over the past two weeks, I have continued working on my previous task and improved it further.

## Apply colorblind_safe more
In my previous work, I applied colorblind_safe to some functions. I have extended this to many more functions. However, in the previous changes, I did not choose colormaps based on what the user wants to visualize. For example, if you are interested in the variation of values, it is better to use a sequential colormap, whereas if the focus is on whether values take certain values, a diverging colormap is more suitable. I have modified each function to use suitable colors. Please take a look at the following examples: hinton and sphereplot.

<img src="https://github.com/qutip/qutip/assets/72233550/c92c7f5a-939f-4a61-a6ef-0098094ac836" width="400px">\
hinton, colorblind_safe = False\
<img src="https://github.com/qutip/qutip/assets/72233550/e9e6bb0e-487d-4ccf-9c0e-f74f35c5283b" width="400px">\
hinton, colorblind_safe = True\
<img src="https://github.com/qutip/qutip/assets/72233550/76cad290-1211-454a-865e-cd6561de61bd" width="400px">\
sphere_plot, colorblind_safe = True\
<img src="https://github.com/qutip/qutip/assets/72233550/ab147971-d5f3-4cc4-b875-afede25644b2" width="400px">\
sphare_plot, colorblind_safe = True

## Prepare for the first evaluation
The first evaluation for GSoC is coming. Therefore, in addition to making the code mergeable, I have also updated the documentation. I am excited to see it being merged and used by everyone. If you have any ideas to make it even better, let's contribute to QuTiP.