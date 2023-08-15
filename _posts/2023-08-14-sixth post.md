# Making animation functions useful

## merging plot functions and animation functions
First, I integrated the plot functions and animation functions. Two weeks ago, I introduced them to you all. Actually, the code for them was almost identical to that of plot_functions. The reason for this was that we couldn't call and use plot_functions within animation functions for the sake of speed and ease of use. However, repeatedly using the same code makes maintenance difficult. Therefore, in the current implementation, the behavior of functions changes depending on whether they receive a Qobj or a list of Qobjs. For instance, it goes like this:

<img width="700" alt="matrix_histogram" src="https://github.com/qutip/qutip-tutorials/assets/72233550/e9cd3d38-8d31-45a3-ac0b-94409ff78bf2">

<div><video controls src="https://github.com/qutip/qutip-tutorials/assets/72233550/39d7b115-ad02-4dfc-a300-0cf74ca67912" muted="false"></video></div>

However, there's a feedback that this makes users to hard to find the animation feature. I plan to recreate the animation functions, and by calling the plot functions internally, even though plot functions will create an animation, the user can use plot functions when they want to make a plot and the other one for animations. This has the advantage of being more intuitive for the user.

## writing a tutorial notebook
Currently, I am creating a tutorial notebook. There are two reasons for this:
Firstly, Jupyter notebook is not compatible with videos. You can easily view animations created by matplotlib using the %matplotlib notebook command. However, some users can't use this command. From my tests, people using Linux or Google colab cannot view videos in this way. We intend to introduce a method in the tutorial notebook that allows such users to easily view videos.
Secondly, handling the axes object is challenging. If you wanted to add a title after creating a video, you would need to proceed with a code like the following:

<div><video controls src="https://github.com/qutip/qutip-tutorials/assets/72233550/9df92d07-7b52-49ed-9dfc-f77effe36805" muted="false"></video></div>

For those unfamiliar with matplotlib, this is too complicated.
By creating a tutorial notebook, I want to help users maximize the potential of QuTiP.