# Two Weeks Progress: PR Merging, Function Enhancement, and Pytest Introduction
Hello, today I will introduce what I've accomplished over the past two weeks.

## PR merged
The first PR #2170 was merged into my project. You can see what was added to functions from my previous posts. This will be released in the next version of qutip, so it will not be available if you install qutip using ```pip install qutip```. To actually use it, you need to execute the following code to download and use it from GitHub.

```
# uninstall qutip if you installed
pip install git+https://github.com/qutip/qutip.git@master
```

## Combining matrix_histogram and matrix_histogram_complex
I worked on combining matrix_histogram and matrix_histogram_complex, two functions visualize different parts of Qobj's matrix. Moreover, matrix_histogram provided users with more options. Therefore, I've been working hard to consolidate these two functions into one and add new features to enable users to visualize more aspects of the matrix properties.

<img width="894" alt="matrix_histogram" src="https://github.com/qutip/qutip/assets/72233550/a4c94bba-06f8-474f-b6cf-88e0385d7d5a">

## Adding pytest
I also added pytest. Until now, visualization did not have tests. This made it difficult for maintainers to notice if there were bugs in the functions within visualization.py or if changes in the modules which they uses break them. By introducing pytest, we can quickly notice and fix these issues.

## Next work
We often want to see the time evolution of a system. '''Quite.solver.Result''' class allows us to have the state of such systems. For example, '''plot_expectation_values''' is suitable for plotting the expectation values of such systems. However, if the user wants to visualize the time evolution of the density matrix of such a system, they have to create their own animation, although the animation function provided by matplotlib is often difficult to use. I am working on providing a function that allows the user to easily create animations by simply passing the results, while at the same time allowing them to edit the animation settings.
