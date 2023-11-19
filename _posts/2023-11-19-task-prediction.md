---
layout: post_with_comments
title:  "Automatically Estimating Sprint Tasks"
date:   2023-11-19 20:10:00 +0000
categories: blog
---

In your development career, did you ever find yourself in a situation where you have to estimate the time to complete a certain task? Maybe your manager wants to know how long it will take you to complete something. Or maybe you find yourself managing a team of developers and have to report that your team is on track to meet quarterly objectives. Predicting the time it takes to complete something is hard. More often than not, you will find yourself dealing with unpredictable events that can affect your initial predictions. 

Throughout the years, the Agile development methodology has become the de-facto standard for development. Its increase in popularity was mainly influenced by greater flexibility and incremental development approaches, which made it very appealing when compared to alternatives such as the Waterfall Model. Despite the many advantages of Agile software development, it also requires developers and managers to quickly adapt to an ever-changing landscape of requirements. This sometimes results in changing priorities and more time dedicated to task estimations.

Streamlining the planning process in Agile development would prove highly advantageous for teams and companies. Therefore, having an unsupervised tool able to provide such estimates with a certain degree of confidence could bring huge benefits to the industry. It would not only allow developers to provide better work estimates, but also allow managers to plan better roadmaps. This article explores the possibility of building such a tool.


## The Agile Mantra
For over a decade, the Agile methodology has played a vital role in shaping the landscape of software development. It has proven to be a very effective method for developing software, given its fast adaptation to requirement changes and incremental development approach. The increased contact with customers guarantees the end product is less likely to suffer large structural changes later in the development cycle, which reduces the overall cost of development.

However, despite its many benefits, Agile also requires development teams to quickly adapt to requirement changes. Doing this early in the development cycle has little impact, as development teams can quickly adjust the architectural design to meet expectations. Nevertheless, these changes can also occur later in the development, which results in more planning time and the creation of tasks to fulfil the necessary requirements. The time required for the planning and estimations will naturally depend on the complexity of the software. 

Furthermore, the accuracy of such estimations will also depend on the experience of the development team. The more experienced the development team, the more accurate the estimations are. Still, even with an experienced team, it is hard to sometimes relate story point estimates with time taken within a sprint. This can sometimes lead to overestimations and, in some cases, spillovers. Having a spillover is not necessarily a negative indicator of a team’s performance, but could also suggest that the initial story points did not reflect the amount of work necessary to complete a task. 

We believe having a system that could gather and analyse this data could provide large benefits to the software industry. Creating a relation between estimated story points and time to complete those story points could largely improve task estimations.


## Estimation Accuracy
There are a lot of variables at play when estimating a task. One variable that was previously mentioned is the experience of the development team. More experienced developers can detect possible barriers for task development early on. Given the knowledge a developer has of the project and/or the technology being used, they can decide to separate a task into several subtasks, sometimes allowing for more developers to work on it in parallel. This not only creates a clear breakdown of the work, but can also greatly increase the speed of development. On the other hand, a less experienced developer may not do such a breakdown, resulting in longer development and review times. This most likely the aspect that can affect task estimation the most.

Besides developer experience, there are also unpredicted events that can occur during development. These can be in the form of infrastructure downtime, preventing developers to deploy their changes for testing. Furthermore, unplanned events, such as outages, can largely affect the development time of ongoing tasks in a sprint. This can sometimes result in blocker tasks being added to the sprint, which can conflict with ongoing tasks and override their priority.

Lastly, there are personal factors that can affect the sprint, such as people's availability. We will not delve too much into this topic here, but it is something to keep in mind while designing the prediction model.

All these factors can end up skewing initial task estimates, making tasks last more than expected. These should be taken into account if the intent is to design an accurate prediction model. In this article, we mostly focus on the aspect of developer experience, as that seems to be the most impactful factor that could influence the prediction model. We may delve into the other factors in a future article.

After discussing the most influential factors that could skew task predictions, we can start detailing how to provide Sprint estimates with a certain degree of confidence. The next sections go over the chosen strategy.


## Estimating Sprint Tasks
Before discussing a possible approach for task estimations, it is important to highlight some assumptions that the model will make when gathering data from sprints:
- The model is assumed to come from a team using the Agile Development Strategy. Each sprint has the same duration as the last.
- The team does not change during the development cycle.
- The model only considers data from past sprints. It will not be updated in real-time and will not consider task re-estimations.

After establishing these assumptions, I started researching for existing solutions. During my research, the most promising approach I found was one discussed by Michael Larionov [[1]](#sources). A key aspect mentioned in this approach is the need to consider the seniority of the development team. This is a crucial factor for our model, as it can largely affect the distribution of sprint estimates.

Larionov’s approach consists of using statistics to estimate sprint tasks. The main thesis of the article is that estimates can be fitted to either a log-normal or a normal distribution. A key factor that influences this is the experience of the development team and their knowledge of the ongoing project. Less experienced development teams tend to have a higher distribution of variance in their estimations, which produces a log-normal distribution of task estimates. More experienced teams tend to be more consistent, allowing their estimates to be fitted to a normal distribution

To better visualize this distribution, let's use a similar Python script to the one used in the original article by Larionov. 

```python
import numpy as np
import matplotlib.pyplot as plt

# Plotting function
def plot_dist(frozen, min, max):
    _, ax = plt.subplots(1, 1)
    x = np.linspace(min, max, 100)
    ax.plot(x, frozen.pdf(x), 'r-', lw=5, alpha=0.6)
```

The script above defines a function `plot_dist`, which plots data in a graph bounded by the values minimum and maximum values`min` and `max`, respectively. Let us now introduce some data to test out the model:

```python
from scipy.stats import norm

# Simulated Sprint Estimations
sprint_point_data = np.array([27, 30, 32, 31, 28, 29, 34, 33, 26, 30])

# Plotting Normal
shape, loc = norm.fit(sprint_point_data)
fitted = norm(shape, loc)

# Calculating p95 value
print(f'95% confidence: {fitted.ppf(0.05)}\n')

plot_dist(fitted, 12, 50);
```
The array `sprint_point_data` from the previous script, contains Sprint estimations for a given team. In this particular example, notice that the input data has little variance, indicating these estimations were likely the output from a more experience development team. For this particular example, we can use a normal distribution, as the distribution of sprint estimates are quite even. The resulting P95 value is equal to ≈25.97. Therefore, we can guarantee with 95% confidence that we can complete 26 story points in one sprint. Below are the results obtained:

<div style="text-align:center">
    <img alt="Normal distribution for Experienced Developers" src="https://miguelmarcelino.github.io/docs/assets/task-prediction/normal-distribution-experienced-team.png">
</div>

<p></p>

However, this would look quite different if we were to use data from a less experienced team. Let us now consider a different set of sprint estimates:
```python
from scipy.stats import norm

# Simulated Sprint Estimations
sprint_point_data_2 = np.array([7, 8, 14, 12, 14, 13, 18, 16, 19, 17, 15, 12, 22, 21, 23])

# Plotting Log-norm
shape, loc, scale = lognorm.fit(sprint_point_data)
fitted = lognorm(shape, loc, scale)

# Calculating p95 value
print(f'95% confidence: {fitted.ppf(0.05)}\n')

plot_dist(fitted, 0, 40);
```
Notice that our data distribution is different from what we analysed. Our first data points show that there were sprints completed with only 7 or 8 story points. This could indicate that the team was getting used to the project, and that estimations were not as accurate. In a scenario like this, fitting the data to a normal distribution would not result in the most accurate output, as our data distribution appears to be right-skewed. Plotting this data showcases should clarify this:

<div style="text-align:center">
    <img alt="Log-Normal distribution for Less Experienced Developers" src="https://miguelmarcelino.github.io/docs/assets/task-prediction/log-normal-distribution-less-experienced-team.png">
</div>

<p></p>

Analysing the distribution of story points is one of the key aspects to consider if the aim is to output accurate estimates. With this in mind, the model should provide an overview of sprint performance (with a certain degree of confidence, that is). If you are a manager, this is probably enough to make you happy, as you can estimate if your team’s quarterly goals are achievable. However, it would be beneficial for developers to have a lower-level overview of these estimates for Sprint planning. So instead of viewing estimations on a Sprint level, we can attempt to apply a similar model on a task level. The next section will explore how we could provide developers with this estimate.


## Creating a Relation between Time and Story Points
We already established that we can use data from previous sprints to approximately estimate how many story points a development team is guaranteed to complete within a sprint. If our model is to be used by developers, it would be beneficial if it could be extended to predict how long a task would take to complete based on its estimated story point count. 
Story points are an abstract measure of complexity. Estimations are based on previously completed user-stories or tasks. This implies there should be a relation between all the user-stories completed with a certain amount of story points. In practice, this effort level should also relate to the amount of hours a user-story has taken to complete. In this section, I will attempt to use statistical modelling to find a correlation between the number of hours and story point estimations.

To make this possible, our model will have to gather data about task estimations and completion time. We should be able to model this in Python using a matrix, where the first column stores story points and the second column stores completion time in hours.

Let's introduce an example that showcases this approach.

```python
from numpy import cumsum
from scipy.stats import lognorm

# A matrix containing the task data in the form 'story_points hours_taken'
task_data = np.matrix('1 2; 3 8; 5 12; 5 12; 3 6; 2 4; 1 3; 2 6; 8 17; 5 10; 5 16; 5 12; 5 12; 5 14; 5 11; 8 14; 8 9; 8 10')

# Retrieve estimations
task_estimations = np.array(task_data[:,0])
estimations_with_indices = np.unique(task_estimations, return_counts=True)
estimations = estimations_with_indices[0]
counts_by_estimation = estimations_with_indices[1]

# Compute the split sizes
split_sizes = cumsum(counts_by_estimation)

# Split array by story point estimation 
sortedv1 = np.sort(task_data, axis=0)
list_sorted = task_data[np.apply_along_axis(lambda row: row[:, 0], 1, task_data).argsort()][0]
split_array = np.split(list_sorted, split_sizes[:len(split_sizes)-1], axis=0)

# Get position that matches story points 
#    We need to select positions [0][0], as np.where returns a tuple, such as (array([x], dtype=int64),)
#    We want the first element, which returns an array containing the possible values. 
#    Given our previous conditions, we know there should only be 1, so we select the first element
position = np.where(estimations==5)[0][0]
task_hour_data = np.array(split_array[position][:,1]).flatten()

# Plotting Norm for tasks
shapeTask, locTask, scaleTask = lognorm.fit(task_hour_data, floc=0)
fittedTask = lognorm(shapeTask, locTask, scaleTask)

print(f'P95: {fittedTask.ppf(0.05)} hours')

plot_dist(fittedTask, 0, 25);
```

As said previously, we can use a matrix to represent a relation between story points and task completion time. In our example above, this data is storted in `task_data`. To process this data, I started by separating it into a set of sub-matrices, each containing the data regarding individual story point estimations. To help you visualize this approach, consider the following matrix:

```python
np.matrix('3 5; 3 8; 4 2')
```

From this initial matrix, I retrieve the sub-matrices `[3 5; 3 8]` and `[4 2]`, therefore gathering all the data for each story point estimate. In the code above, this is the result of the `split_array` variable. 
Using this approach to retrieve sub-matrices, I can then retrieve all the data that matches a certain story point estimation. In the example above, I chose `5` as my story-point target. I can then get all the data related to completion time and plot it using the `plot_dist` function we used in the example from the previous section. 
In our case, the data is not right-skewed, so we should be able to use a normal distribution. Plotting the data gives us the following result:


<div style="text-align:center">
    <img alt="Normal distribution of Task Prediction" src="https://miguelmarcelino.github.io/docs/assets/task-prediction/normal-distribution-task-time-prediction.png">
</div>

<p></p>

Additionally, we can calculate our P95 values, which in this case output a value of ≈9.53. In this case, this means we need at least 9 hours to successfully complete a task with 95% guarantee. 
This more granular approach should allow developers to estimate and plan sprints with a higher degree of confidence.

It is important to mention that the previous model is rather simple and could be extended with more variables to make it more accurate. For instance, if you know the developer that is going to work on a given task, you could also filter out estimations solely for that developer. This would likely create a more accurate time estimation for a given task. We purposefully left this out, given that it is not common to pre-assign tasks to certain developers before the sprint starts. This could be considered as an extension if you want to adapt your model in real time once the sprint has already started.

Despite this approach offering a more granular overview of work progress, it still does not tell the whole picture. Tasks typically have dependencies between them, which affect how developers plan Sprints. In order to have a full overview of how many tasks we could add to a sprint, we would need to take these dependencies into account. The next section briefly discusses this and presents a possible solution.

## This is only 50% of the problem…
Our model is now predicting how long tasks take based on their estimated story points. Let us assume that we have been gathering story point data for some time now. This means our estimates should now be more accurate than when we started, as we managed to even out any outliers. Having this information is only half of the problem. The largest benefit would come in the form of predicting whether the tasks developers are adding to the next sprint could end up taking more time than the sprint’s total duration. To successfully calculate this, we would need to consider two factors:
- The size of the development team and
- Task dependencies

Visualizing these dependencies could be done in a Gantt chart. This model should allow developers to detect possible spillovers when planning a sprint. We will not provide a full implementation of this approach in this article, but we can at least visualize what it would look like using a Gantt chart. Let us consider a small team comprised of 3 developers developing in sprints of 2 weeks.

<div style="text-align:center">
    <img alt="Gantt Chart" src="https://miguelmarcelino.github.io/docs/assets/task-prediction/gantt-chart.png">
</div>

<p></p>

The model above illustrates a possible task assignment for a two-week sprint. Each of the three developers is assigned a different colour. In our example, we do not allow developers to be working on more than one task at a time. This explains why there are no overlapping colours.
Tasks that have multiple colours are assigned to multiple developers, where each colour represents one developer. 
Lastly, all tasks that are highlighted red exceed the time of the sprint, according to the prediction model. We can see one task where this happens, which exceeds the Sprints assigned time by 1 day. Having this information during sprint planning could enable developers to make more informed decisions in selecting tasks that align optimally with the designated sprint timeframe.

## Future Work
The aim of this article was to discuss a possible approach to streamline the planing process in Agile project development. In the previous sections, we discussed a potential statistical model that could help predict the running time for tasks. Nevertheless, as the goal is to develop an automated tool capable of executing unsupervised estimations, there is also a necessity to automate the retrieval of Sprint data.

Most companies these days use tools, such as Jira, to plan their sprints. A possible way to automate the previous approach, would be to systematically retrieve data from such platforms and update the statistical model.
Doing so in real-time would likely have increased running cost, as we would constantly be updating the model. As a first iteration, we could do this at the end of each Sprint. This would avoid responding to events, such as task re-estimations, which could have a large impact in performance (granted, these should be very minor if the sprint was properly planned). 

If this model was to be used long-term, we would also have to think of a way to avoid retrieving all past sprint data. Throughout this article, we have assumed that all the sprint data was available for our model. In an ideal scenario, we would just be able to update the model based on the information from new tasks. 

We leave these thoughts as potential future improvements for the presented approach.

## Final thoughts
Overall, it seems it might be possible to estimate task running time with a certain degree of confidence, but we are yet to confirm if we can use it on a greater scale. Retrieving the data from a third-party tool seems to be a feasible approach, but processing it on a large scale presents several concerns. Furthermore, we have yet to discover if we could use the information from this model to start predicting tasks without requiring inputs from developers. We leave this as future work.

Despite the drawbacks, the adoption of a statistical model has the potential to yield substantial advantages for agile development teams, providing them with a tool capable of speeding up sprint planning. Moreover, it could offer an elevated level of assurance to managers, giving them the ability to plan more accurate road maps. 


## Sources
- [Using Statistics for Agile Estimations](https://github.com/mlarionov/machine_learning_POC/blob/52cdece108f285a4e67212fd289f6dbf9035dca0/agile_estimation/agile_estimation_2.ipynb)
