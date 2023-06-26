# Aplly colorblind_safe and arrange arguments
Hello. Today, I will introduce what I have been working on for the past two weeks.

## colorblind safe
Firstly, it is about color settings. Previously, even when 'qutip.settings.colorblind_safe=True,' most functions did not have the capability to change colors. So, I have been modifying the functions to support this. You can see actual usage examples [here](https://drive.google.com/file/d/1LSNLWW2FBhX4PeMXJTxSN6Qgb-G6_TXn/view). By simply setting 'colorblind_safe=True,' you can see that the colors are automatically changed.

<img src="https://github.com/tamakoshi2001/tamakoshi2001.github.io/assets/72233550/f30373b4-4b6e-4e3b-a4a1-e51ea547cdda" width="300px">\
colorblind_safe = False

<img src="https://github.com/tamakoshi2001/tamakoshi2001.github.io/assets/72233550/e5c1237a-b4b0-4c3c-a9a6-67e1ed66ed7c" width="300px">\
colorblind_safe = True

## change arguments
Next, I have been changing the variables in the functions. The issue with the previous functions can be seen by comparing the following two functions:

1. hinton
```
def hinton(rho, xlabels=None, ylabels=None, title=None, ax=None, cmap=None,
           label_top=True, color_style="scaled"):
    """Draws a Hinton diagram for visualizing a density matrix or superoperator.
...
```
2. plot_wigner_sphere
```
def plot_wigner_sphere(fig, ax, wigner, reflections):
    """Plots a coloured Bloch sphere.
...
```

By comparing these two functions, you can see the following: The first is that the order of arguments is different between the functions. The second is that there are arguments, such as 'title,' that are included in one but not the other. I am currently fixing this. Specifically, I am making the following modifications:

The variables are arranged in the order of mandatory variables specific to the function, optional variables specific to the function, and variables that are common to many functions. Additionally, I am removing arguments like 'title' that can be set later by the user. Here is the example of my change;
```
def hinton(rho, color_style="scaled", label_top=True, *,
           xticklabels=None, yticklabels=None, cmap=None, colorbar=True,
           figure=None, axes=None):
    """Draws a Hinton diagram for visualizing a density matrix or superoperator.
...
```

With these changes, I am confident that users will be able to use the functions consistently.

Currently, I am applying these modifications to as many functions as possible. I will inform you about the results in the next post."
