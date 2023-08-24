## 1. Personal Background
Name: Yuji TAMAKOSHI<br>
Location: Japan<br>
School: 4th year undergraduate student at the University of Tokyo, Department of physical engineering<br>
GitHub: tamakoshi2001, https://github.com/tamakoshi2001<br>
Email: uotstudent2001@g.ecc.u-tokyo.ac.jp or tamakosiy@gmail.com<br>
Phone: +81 (0)70-8367-2723
## 2. Goals of this project
### 2-1. Improving plot functions
The first goal is to improve plot functions. Before this project, the arguments of functions were not well organized. For example, you couldn’t set `figsize` in `plot_wigner`, but not in `plot_wigner_sphere`. This prevented users from using them intuitively. Also, QuTiP has `colorblind_safe` as an option to make itself useful for people suffering from color blindness, but most functions do not use it.
### 2-2. Creating animation functions
The second goal is to create animation functions. The time evolution of quantum states is an important part of quantum physics and QuTiP has many functions to calculate it fast and easily. Animation functions help users to quickly visualize it and make QuTiP more useful.
## 3. My contribution
### 3-1. Improving plot functions
#### 3-1-1. Selecting arguments
We discussed which variables should be kept, which should be added, and how they should be arranged to make the plot functions user-friendly. We decided to place the variables in the order of essential variables for the function, function-specific optional variables, and common variables.
#### 3-1-2. Coding
Here is an example of my coding. In this case, this function works only with `wigner` so it is the first argument. `reflection` adds reflections to a plot and is unique to this so set as the second argument. Other arguments are common and many users want to add them to customize the plot. They are set as keyword-only arguments. Other functions are coded in the almost same way.
```python
plot_wigner_sphere(fig, ax, wigner, reflections)
```
before
```python
plot_wigner_sphere(wigner, reflections=False, *, cmap=None, colorbar=True, fig=None, ax=None)
```
after<br>
Also, coding includes deleting and merging functions. For example, I deleted `plot_wigner_fock_distribution` and combined `plot_spin_distribution_2d` and `plot_spin_distribution_3d` into `plot_spin_distribution`.
We want to talk about `qutip.settings.colorblind_safe`. When you set it as True, most functions change their colors automatically.
```python
import qutip
rho = qutip.rand_dm(5)
# default
qutip.settings.colorblind_safe = False
fig, ax = qutip.matrix_histogram(rho, limits=[0, 1]);
```
a matrix histogram of real part of a random operator with colorblind_safe is False<br>
<img width="700" alt="matrix_histogram" src="https://github.com/tamakoshi2001/tamakoshi2001.github.io/assets/72233550/b870d6ec-ac4a-498c-9b93-85df5eaa2811">
```python
qutip.settings.colorblind_safe = True
fig, ax = qutip.matrix_histogram(rho, limits=[0, 1]);
```
a matrix histogram of real part of a random operator with colorblind_safe is True<br>
<img width="700" alt="matrix_histogram" src="https://github.com/tamakoshi2001/tamakoshi2001.github.io/assets/72233550/88a578ff-bb2f-440e-ab9a-a5bd349c3870">
#### 3-1-3. Adding tests
I added tests to cover all functions in `visualization.py`. QuTiP did not have tests for them, but the coverage is over 90% now.
#### 3-1-4. Updating docs and tutorials
I changed the doc and tutorials to follow my change.
### 3-2. Creating animation functions
#### 3-2-1. Research
I researched how to create animations with `matplotlib`. Although `matplotlib` offers `Artistanimation` and `Funcanimation`, in order for users to use them easily and for maintainers to maintain them effectively, it's essential to understand how they works correctly.
#### 3-2-2. Discussion about the way to implement
We discussed the implementation. Due to the speed of function execution and the fact that users can use it in the same way as they use plot functions, we decided to implement animation functions using `Artistanimation`.
#### 3-2-3. Coding
Animation functions are defined in `animation.py` and they are wrapper functions of plot functions. They work differently when users pass an object or a list of objects. Here is the code of `matrix_histogram`. It return a plot when it has an object. When it has a list of objects, it returns an `ArtistAnimation` object. This object needs a list of collections of `artist` objects and one collection makes one frame. In case of the `bar3d` function, it returns `Poly3DCollection` which is a subclass of artist. Different plot functions return different objects so I carefully read the document and coded.
```python
        artist = ax.bar3d(xpos, ypos, zpos, dx, dy, bar_M, color=colors,
                          edgecolors=options['bars_edgecolor'],
                          linewidths=options['bars_lw'],
                          shade=options['shade'])
        artist_list.append([artist])

    if len(Ms) == 1:
        output = ax
    else:
        output = animation.ArtistAnimation(fig, artist_list, interval=50,
                                           blit=True, repeat_delay=1000)
```
inside of matrix_histogram<br>
This is a simple animation of a time evolution of a state.
```python
from qutip import ket, sigmaz, tensor, qeye, mesolve, anim_schmidt
import numpy as np
import matplotlib.pyplot as plt
%matplotlib notebook
H = tensor(sigmaz(), qeye(2))
psi0 = ket('10') + ket('01')
psi0 = psi0.unit()
tlist = np.linspace(0, 3*np.pi, 100)
results = mesolve(H, psi0, tlist, [], [])
fig, ani = anim_schmidt(results)
```

<div><video controls src="https://github.com/tamakoshi2001/tamakoshi2001.github.io/assets/72233550/165fb08a-15ec-46df-80a1-6497b2e90c72" muted="false"></video></div>

#### 3-2-4. Adding tests
I added tests to cover all functions in animation.py.
#### 3-2-5. Writing a tutorial notebook
I wrote a tutorial notebook to explain the way to use the functions because they are useful, but difficult to customize.
## 4. The current state
I completed all the tasks. My work is in the 6th section.
## 5. What is left to do
This project completed all tasks. Nothing is left.
## 6. Code got merged
### 6-1. Improving plot functions
[Organize arguments of functions and apply colorblind_safe option](https://github.com/qutip/qutip/pull/2170)<br>
[pytest for visualization.py](https://github.com/qutip/qutip/pull/2192)<br>
[change for plot_wigner_sphere and matrix_histogram_complex](https://github.com/qutip/qutip/pull/2193)<br>
[sort args of sphereplot](https://github.com/qutip/qutip/pull/2219)<br>
[change notebook to follow qutip PR#2170](https://github.com/qutip/qutip-tutorials/pull/66)<br>
[delete matrix_histogram_complex](https://github.com/qutip/qutip-tutorials/pull/68)
### 6-2. Creating animation functions
[add animation functions](https://github.com/qutip/qutip/pull/2203)<br>
[add animation demo](https://github.com/qutip/qutip-tutorials/pull/67)
## 7. Challenges
### 7-1. Keeping thinking about what code is good
The first one was questioning whether my code was optimal. The code I wrote would be used by many people, and Someone might add new things in the future. Therefore, it's crucial to write code that is user-friendly and extensible. While there's no definitive answer to what code meets them, I did my best through discussions with my mentor.
### 7-2. Understanding Python
The second challenge was that the technology I used for implementing new features was more complicated than it appeared. I developed a function to create animations using `matplotlib`, but to effectively generate the videos, I needed to understand object-oriented programming and how `matplotlib` functions are implemented based on that. Moreover, I had to make animation functions in harmony with the existing functions in QuTiP. I changed the implementation multiple times to make good functions.
## 8. Things I learned
### 8-1. The official documents
The first was the significance of official documentation. First, I tried to understand `matplotlib` by reading tech blogs written by others. However, this approach proved insufficient, and I realized that I needed a deeper understanding to make functions using `matplotlib`. The official document helped me a lot. Of course, I added explanations and made a tutorial notebook for my new functions so that users understand them well.
### 8-2. Communication
The second lesson was the importance of communication. I frequently discussed my code and the progress of my project with my mentor, both in meetings and through text chats. Thanks to these interactions, I was able to refine my code and successfully complete my project on schedule.
## 9. Acknowledgment
I'd like to thank Google for giving us a wonderful opportunity to start to contribute to OSS and my mentors [Eric Giguere](https://github.com/Ericgig) and [Neill Lambert](https://github.com/nwlambert) for helping me completing this project.

Through GSoC2023, I learned about software development from planning a project to collaborating to achieve it. I will continue to do what I can to the community by making use of this experience.
