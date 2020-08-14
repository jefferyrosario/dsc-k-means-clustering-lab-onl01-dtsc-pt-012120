<<<<<<< HEAD

# Setting up a Professional Data Science Environment - Setup

## Introduction

In this lesson, you'll continue setting up your professional data science environment by making a virtual environment. 

## Objectives

You will be able to:
* Use basic commands to navigate the command line
* Summarize why virtual environments are used
* Use a virtual environment

## Cloning this Repository

To finish this setup process, you’re going to need to download a copy of the files in this repository. To do that, you need to start by opening a terminal window.

If you’re on a Windows machine, select “Git Bash” from either the start menu or the search bar and it’ll open up a terminal (don’t use the default Windows terminal - it will not work for this).

If you’re working on a mac, open the “Terminal” app in the “Utilities” folder within your “Applications” folder.

Let’s type `pwd` to “print the working directory. It should be somewhere you are OK downloading files to. If not, feel free to use the “cd” command to change directory to one you’d like to work from.

Then type (or better still, cut and paste) `git clone git@github.com:learn-co-curriculum/dsc-data-science-env-setup-v2-1.git`

*In Windows, in git bash, to paste from the clipboard the shortcut should be `ctrl-shift-insert`*

This will create a new subdirectory whose name starts with "dsc-data-science-env-setup-v2-1" which will contain a copy of all of the files from this repository. Go into that directory using the `cd`, or change directory, command (after typing `cd dsc` you should be able to hit the **tab** key to "tab complete" so you don't need to type the whole directory name). That should work on both Windows and Macs.

## Setting Up Virtual Environments

As you do data science projects, you will spend a lot of your time using pre-written libraries to speed up your development. Examples include NumPy, Pandas and scikit-learn. As you work on different projects, you may also find that you end up using different versions of different libraries for different projects. The most common versioning issue is that some projects will run in Python 2 whereas others will run in Python 3, but you may also find that different projects depend on different versions of libraries like Tensorflow.

Occasionally, code that works in an old version of a library won’t work in a newer version. So if you open up a new project and install the dependencies, it’s possible that your old project won’t work anymore.

To avoid that problem, a best practice is to use “virtual environments”. Virtual environments allow you to have different versions of Python and different versions of the various libraries you use, so you can install a new version of a library for one project but still use the old version for another project. It’s almost as if you have multiple computers that you can swap between, each having a different setup and configuration, just by running a couple of commands.

There is a built-in virtual environment feature in Python, but we’re going to use the more flexible virtual environments provided by Conda as part of the Anaconda distribution you installed.

To use a new virtual environment, there are two steps you need to complete. The first step is to create the virtual environment. That may take a couple of minutes as your computer has to download the necessary version of Python and all of the libraries that you want to be able to use in that environment. The next step then is to “use” the virtual environment by activating it.

If you want to learn more about Conda environments, have a look at the [documentation](https://conda.io/docs/user-guide/tasks/manage-environments.html), otherwise, let’s give this a try.

You need to start by navigating into the root of this project folder, so you’re going to want to type `cd dsc-data-science-env-setup-v2-1` in your terminal if you didn't already.

Then to create the environment, on a mac, type `conda env create -f environment.yml`. On windows, type `conda env create -f windows.yml`. Depending on the speed of your computer and your internet connection it may take up to five minutes for this to complete. While it does you should see output similar to that displayed below start to appear in your terminal.

<img src='http://curriculum-content.s3.amazonaws.com/data-science/screen-47.png' width="750">

Next, try activating the environment. Whether you're on a Mac or using git bash on a windows machine, type `conda activate learn-env` (if you have an issue with running git bash, the command to activate Conda within the Conda shell on windows is `activate learn-env`).

To confirm that it worked, type `conda info --envs` and confirm that the output in the terminal ends with /learn-env - e.g. *  /Users/peterbell/anaconda3/envs/learn-env

#### Troubleshooting
If you see a message that states “WARNING: A newer version of Conda exists”, run `conda update -n base conda` and then try again to create the environment using `conda env create -f environment.yml`.

If you see a message that states "file not found", double check that you are running this command from the directory that contains the .yml file. If you type `ls` you should see the .yml file. If you don't see it, you likely forgot to run `cd dsc-data-science-env-setup-v2-1` to change into the right directory.

## Setting your Default Environment

You have successfully created your virtual environment! To be sure that you are using the learn-env, it's helpful to set it as your default environment so that you don't need to remember to manually switch to it every time you open terminal. This step is suggested but not required.

<details>
<summary>Mac</summary>
On a Mac, run `echo "conda activate learn-env" >> ~/.bash_profile` to add the configuration to your bash profile and then run `source ~/.bash_profile` to activate the changes you just made.
</details>

<details>
<summary>Windows</summary>
To follow these instructions on a Windows machine you must be using the Git Bash shell it was suggested to install above.
Run `touch ~/.bash_profile` to create a new file. Next, run `echo "conda activate learn-env" >> ~/.bash_profile` to add the configuration to your bash profile and then run `source ~/.bash_profile` to activate the changes you just made.
</details>

## Updating your Virtual Environment

Every so often we create new versions of the virtual environment and we'll ask you to update your virtual environment. To do that, download the latest version of this repository with the latest changes. Then go into a terminal window and:
```
conda activate base # To make sure you're not in the learn-env environment
conda remove -n learn-env --all # To get rid of the environment
conda env list # Make sure it doesn't list learn-env - if it does, try the last step again
# Then to re-create the environment from the latest environment file
# On a Mac
conda env create -f environment.yml
# Or in Windows
conda env create -f windows.yml

```

## Configuring your Kernel

Jupyter Notebooks run "kernels" - the computational engine used for executing your code. It's important to be running the right kernel within your notebook, otherwise you may get errors stating that you don't have a particular package or have the wrong version of it or even complaints about the version of Python you're running (some packages that work with Python 3.6.6 don't currently support Python 3.7, for example).

It is essential to run `conda activate learn-env` (if you have an issue with running git bash, the command to activate Conda within the Conda shell on windows is `activate learn-env`) every time you start a new terminal window that you are going to use to either run a Jupyter Notebook or your tests. If you don't do this you **will** get errors, so please check this first. If you are not sure whether you have activated the environment, in the terminal type `conda list -f obscure` and it should show you that you have v1.0.1 of the "obscure" package. If it doesn't show that, (re)run (`conda`) `activate learn-env`.

However, there is one more step you need to perform. Firstly you need to ensure your terminal is running the learn-env virtual environment so you have the necessary packages. Then you need to go into your Jupyter Notebook and when viewing a notebook, click on "Kernel" in the top bar, then "Change Kernel" and then pick the learn-env kernel. You must make sure you're running the learn-env kernel whenever you're working in a Jupyter Notebook.

If for any reason you don't see the learn-env option in the drop-down list of kernels, exit the notebook in the browser, close down the notebook server, and in the terminal type `python -m ipykernel install --user --name=learn-env` - that will add the learn-env to your list of kernels and when you restart the Jupyter Notebook server and then open a notebook, you'll be able to select the learn-env option from the list of kernels.

## Summary

Congratulations! If you've gotten this far and everything has worked, you have successfully set up a virtual environment which will serve as a great baseline setup for working as a professional data scientist!
=======
# K-means Clustering - Lab

## Introduction

In this lab, you'll implement the k-means clustering algorithm using scikit-learn to analyze a dataset!

## Objectives

In this lab you will: 

- Perform k-means clustering in scikit-learn 
- Describe the tuning parameters found in scikit-learn's implementation of k-means clustering 
- Use an elbow plot with various metrics to determine the optimal number of clusters 


## The K-means Algorithm 

The k-means clustering algorithm is an iterative algorithm that reaches for a predetermined number of clusters within an unlabeled dataset, and basically works as follows:

- Select $k$ initial seeds
- Assign each observation to the cluster to which it is the "closest" 
- Recompute the cluster centroids
- Reassign the observations to one of the clusters according to some rule
- Stop if there is no reallocation 


## Create a Dataset

For this lab, we'll create a synthetic dataset to work with, so that there are clearly defined clusters we can work with to see how well the algorithm performs. 

In the cell below:

* Import `make_blobs` from `sklearn.datasets`
* Import `pandas`, `numpy`, and `matplotlib.pyplot`, and set the standard alias for each  
* Set matplotlib visualizations to display inline
* Use `numpy` to set a random seed of `1` 
* Import `KMeans` from `sklearn.cluster`


```python
# Your code here
```

Now, we'll use `make_blobs()` to create our dataset. 

In the cell below:

* Call `make_blobs()`, and pass in the following parameters:
    * `n_samples=400`
    * `n_features=2`
    * `centers=6`
    * `cluster_std=0.8`


```python
X, y = None
```

Now let's visualize our clusters to see what we've created. Run the cell below to visualize our newly created dataset.


```python
plt.scatter(X[:, 0], X[:, 1], c=y, s=10);
```

The nice thing about creating a synthetic dataset with `make_blobs()` is that it can assign ground-truth clusters, which is why each of the clusters in the visualization above are colored differently. Because of this, we have a way to check the performance of our clustering results against the ground truth of the synthetic dataset. Note that this isn't something that we can do with real-world problems (because if we had labels, we'd likely use supervised learning instead!). However, when learning how to work with clustering algorithms, this provides a solid way for us to learn a bit more about how the algorithm works. 

## Using K-means

Let's go ahead and instantiate a `KMeans` class and fit it to our data. Then, we can explore the results provided by the algorithm to see how well it performs. 

In the cell below:

* Instantiate the `KMeans` class, and set `n_clusters` to `6` 
* Fit `KMeans` to the data stored in `X` 
* Predict which clusters each data point belongs to 


```python
k_means = None

predicted_clusters = None
```

Now that we have the predicted clusters, let's visualize them and compare to the original data 

In the cell below: 

* Create a scatter plot as we did up above, but this time, set `c=predicted_clusters`. The first two arguments and `s=10` should stay the same  
* Get the cluster centers from the object's `.cluster_centers_` attribute  
* Create another scatter plot, but this time, for the first two arguments, pass in `centers[:, 0]` and `centers[:, 1]`. Also set `c='black'` and `s=70` 


```python

centers = None

```

**_Question:_**

In your opinion, do the centroids match up with the cluster centers?

Write your answer below this line:
_______________________________________________________________________________



## Tuning Parameters

As you can see, the k-means algorithm is pretty good at identifying the clusters. Do keep in mind that for a real dataset, you will not be able to evaluate the method as such, as we don't know a priori what the clusters should be. This is the nature of unsupervised learning. The scikit-learn documentation does suggest two methods to evaluate your clusters when the "ground truth" is not known: the Silhouette coefficient and the Calinski-Harabasz index. We'll talk about them later, but first, let's look at the scikit-learn options when using KMeans.

The nice thing about the scikit-learn's k-means clustering algorithm is that certain parameters can be specified to tweak the algorithm. We'll discuss two important parameters which we haven't specified before: `init` and `algorithm`.

### 1. The `init` parameter

`init` specifies the method for initialization:

- `k-means++`: is the default method, this method selects initial cluster centers in a smart way in order to pursue fast convergence 
- `random`: choose $k$ random observations for the initial centroids 
- `ndarray`: you can pass this argument and provide initial centers 

### 2. The `algorithm` parameter

`algorithm` specifies the algorithm used:

- If `full` is specified, a full EM-style algorithm is performed. EM is short for "Expectation Maximization" and its name is derived from the nature of the algorithm, wherein each iteration an E-step (in the context of K-means clustering, the points are assigned to the nearest center) and an M-step (the cluster mean is updated based on the elements of the cluster) is created 
- The EM algorithm can be slow. The `elkan` variation is more efficient, but not available for sparse data 
- The default is `auto`, and automatically selects `full` for sparse data and `elkan` for dense data 

### Dealing With an Unknown Number of Clusters

Now, let's create another dataset. This time, we'll randomly generate a number between 3 and 8 to determine the number of clusters, without us knowing what that value actually is. 

In the cell below:

* Create another dataset using `make_blobs()`. Pass in the following parameters:
    * `n_samples=400`
    * `n_features=2`
    * `centers=np.random.randint(3, 8)`
    * `cluster_std = 0.8`


```python
X_2, y_2 = None
```

Now we've created a dataset, but we don't know how many clusters actually exist in this dataset, so we don't know what value to set for $k$!

In order to figure out the best value for $k$, we'll create a different version of the clustering algorithm for each potential value of $k$, and find the best one using an **_Elbow Plot_**.   


In the cell below, instantiate and fit `KMeans` with a different value for `n_clusters` between 3 and 7, inclusive.

Then, store each of the objects in a list. 


```python
k_means_3 = None
k_means_4 = None
k_means_5 = None
k_means_6 = None
k_means_7 = None

k_list = None
```

Now, in the cell below, import `calinski_harabasz_score` from `sklearn.metrics`. 


```python
# Your code here
```

This is a metric used to judge how good our overall fit is. This score works by computing a ratio of between-cluster distance to inter-cluster distance. Intuitively, we can assume that good clusters will have smaller distances between the points in each cluster, and larger distances to the points in other clusters.

Note that it's not a good idea to just exhaustively try every possible value for $k$. As $k$ grows, the number of points inside each cluster shrinks, until $k$ is equal to the total number of items in our dataset. At this point, each cluster would report a perfect variance ratio, since each point is at the center of their own individual cluster! 

Instead, our best method is to plot the variance ratios and find the **_elbow_** in the plot. Here's an example of the type of plot you'll generate:

<img src='images/wcss_elbow1.png' width = "500">

In this example, the elbow is at $k=5$. This provides the biggest change to the within-cluster sum of squares score, and every one after that provides only a minimal improvement. Remember, the elbow plot will have a positive or negative slope depending on the metric used for cluster evaluation. Time to try it out on our data to determine the optimal number of clusters!

In the cell below:

* Create an empty list called `CH_score` 
* Loop through the models you stored in `k_list`  
    * For each model, get the labels from the `.labels_` attribute 
    * Calculate the `calinski_harabasz_score()` and pass in the data, `X_2`, and the `labels`. Append this score to `CH_score` 


```python
CH_score = None
```

Run the cell below to visualize our elbow plot of CH scores. 


```python
plt.plot([3, 4, 5, 6, 7], CH_score)
plt.xticks([3,4,5,6,7])
plt.title('Calinski Harabasz Scores for Different Values of K')
plt.ylabel('Variance Ratio')
plt.xlabel('K=')
plt.show()
```

That's one metric for evaluating the results; let's take a look at another metric, inertia, also known as Within Cluster Sum of Squares (WCSS). In the cell below:

* Create an empty list called `wcss_score`
* Loop through the models you stored in `k_list` 
    * For each model, get the labels from the `.labels_` attribute 
    * Obtain the `inertia_` attribute from each clustering model and append this value to `wcss_score`  

After creating this, run the cell below it to create a graph.


```python
wcss_score = None
```


```python
plt.plot([3, 4, 5, 6, 7], wcss_score)
plt.xticks([3,4,5,6,7])
plt.title('Within Cluster Sum of Squares')
plt.ylabel('WCSS')
plt.xlabel('K=')
plt.show()
```

**_Question:_**  Interpret the elbow plots you just created. Where are the "elbows" in these plots? According to these plots, how many clusters do you think actually exist in the dataset you created?

Write your answer below this line:
_______________________________________________________________________________

Let's end by visualizing the `X_2` dataset you created to see what the data actually looks like.

In the cell below, create a scatterplot to visualize `X_2`. Set `c=y_2` so that the plot colors each point according to its ground-truth cluster and set `s=10` so the points won't be too big. 


```python
# Your code here
```

We were right! The data does actually contain six clusters. Note that there are other types of metrics that can also be used to evaluate the correct value for $k$, such as the Silhouette score. However, checking the variance ratio by calculating the Calinski Harabasz scores is one of the most tried-and-true methods, and should definitely be one of the first tools you reach for when trying to figure out the optimal value for $k$ with k-means clustering. 

## A Note on Dimensionality

We should also note that for this example, we were able to visualize our data because it only contained two dimensions. In the real world, working with datasets with only two dimensions is quite rare. This means that you can't always visualize your plots to double-check your work. For this reason, it's extra important to be considerate about the metrics you use to evaluate the performance of your clustering algorithm since you won't be able to "eyeball" it and visually check how many clusters the data looks like it has when you're working with datasets that contain hundreds of dimensions!


## Summary

In this lesson, you used the k-means clustering algorithm in scikit-learn. You also learned a strategy for finding the optimal value for $k$ by using elbow plots and variance ratios for when you're working with data and you don't know how many clusters actually exist. 
>>>>>>> bca06c2ea3ba9856d6e302fb4c491169765f4d34
