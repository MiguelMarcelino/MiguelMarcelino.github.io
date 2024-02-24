---
layout: post_with_comments
title:  "Automatic Task Estimation - Thoughts and Ideas"
date:   2024-02-22 20:10:00 +0000
categories: blog
---

After reading some articles on the subject of automatic Agile estimations, I was left with the feeling that no matter the estimation strategy, there is no going around the main issue at hand: The human factor. Despite all research done on the topic of automatic Agile estimation, replacing experts has proven to be a hard problem to solve. Being able to automatically estimate tasks requires tremendous knowledge of, at least, the state of the existing codebase, deployment and testing environments, and external dependencies. This is ignoring other factors, such as availability, the seniority of the development team, and knowledge of the code base. In an ideal world, we would have a development environment with no fluctuations in work scope and a history of very accurate task predictions. Naturally, this is something that is hard to achieve, as work scope can vary drastically, either because of unpredicted side-effects or unforeseen dependencies. Task estimations can only go so far, as they rely on the knowledge available during planning.

Having said that, it might seem like I am a pessimist and don't see this topic advance much in the next years. That is definitely not the case (trust me!), but I do believe there are key aspects that must be considered moving forward and scenarios where automatic estimation might not be ideal. Without any particular order, here are my thoughts on automatic Agile estimations.

## Before diving in...
This is the second article I am writing on the topic of task estimations. In the [first article](https://miguelmarcelino.github.io/blog/2023/11/19/task-prediction.html) I discussed a method developed by Michael Larionov [[1]](#sources), which used a statistical model that I extended to predict the duration of tasks. In this article, I am once again diving deeper into the topic of automatic Agile estimations, but this time expanding the discussion to also cover other estimation methods, such as Monte Carlo estimation methods and Bayesian Networks. This article compiles what I learned when researching this topic.

Throughout the article, I will be presenting my personal thoughts on the topic of automatic Agile estimation. Therefore, expect it to be very subjective, as I am writing things as I see and interpret them. I also have no involvement in any of the projects mentioned. I just happened to stumble upon a curious topic and felt like expressing my opinion and thoughts on the matter.

With that in mind, let us proceed with the discussion on automatic agile estimations.


## The impact of Unknowns
When estimating agile tasks, there will always be aspects we are unaware of during planning. Whether this is because of how complex our software is, or because of how experienced the development team is, there can alsways be unknown factors during task estimation. In this section, we will discuss the impact of unknowns on task estimations. For this discussion, we will separate unknowns in two terms: known unknowns and unknown unknowns. This might sound confusing at first, so let me try to explain it briefly.

Each task has certain key requirements necessary to complete it. When creating a task, you might be aware of some requirements, even though you may not have all the details for them. These will be your known unknowns. To visualize this scenario, consider you are creating a task to implement a new API endpoint. The endpoint will be used to retrieve a history of gas prices stored in an existing database. While planning the task, you identified key requirements, such as the most appropriate protocol to use, the need for validating an incoming request, the required security level, and so on.
After successfully gathering these requirements and creating your task, you add it to the backlog. Your team will then estimate the task during sprint planning and, once everyone has reached a consensus, the task is considered to be ready for development.

Some time has past, and the task you created was added to a sprint and is being actively developed by someone from your team. However, that developer discovers an issue. In your initial proposal, you suggested returning a list containing the full history of gas prices. However, because your system has been storing data for some time now and has no data retention policy, retrieving the whole history in a single request has proven to be a problem. The endpoint keeps timing out waiting for all the results to be available. After re-evaluating your initial implementation, you imediately come to the conclusion you require pagination. So you update your initial set of requirements and have the developer adjust the endpoint to consider it.

You just came accross an unknown unknown. This had sliped through during planing, as you were unaware of the fact the system was storing so much data. Such things can happen and will require you to re-evaluate your initial estimate. 

Coming back to our topic of automatic task estimations, this simple example illustrates why automatic Agile estimations are a hard problem to solve. Estimating tasks requires deep knowledge of the system and potential side effects. In our example scenario, our developer forgot to consider that the database was storing a considerable amount of data, making it almost impossible to retrieve all the data with a single request. But this could become infinitely more difficult when we start to think about the complexity of modern systems. With more complex architectures and an increasing amount of system dependencies, estimating tasks becomes even harder. This becomes even more for automatic agile estimation, as the accuracy of predictions will depend on how accurate past estimations are. Let us explore this topic in the next section.

## Past estimations matter
As discussed previously, unknown unknowns can largely affect the outcome of a task and its initial estimate. Nevertheless, the problem exposed previously with our API example can be escalated throughout time if task estimates are not revisited. Most task estimation models rely on past project data to develop their estimates. Having a good history of estimates is required if we want to benefit the most from an automatic estimation tool.

Following our example from earlier, this would require you to adjust the original estimate done during planning, most likely requiring a re-estimation from the whole team to ensure maximum accuracy. This process is very relevant for an automatic estimation model, as estimation data will be used for future predictions. Ignoring this new scope update could end up skewing future predictions, leading to a less accurate model.

Keeping an up-to-date backlog is essential for automatic Agile estimations. However, there is still another relevant aspect to consider when estimating tasks, which is considering what data will be used to train the prediction models. Injesting all estimation data could lead to inacurate estimations and overall a less usable tool. Using all the data would naturally provide a larger dataset to train the model, but likely produce more generic predictions that would prove less valuable. I dedicate the next section to discuss this topic.

## Partition data before estimating
Arguably the most important conclusion I came to when reading through some articles on the topic of automatic Agile task estimations, was that it is a better investment to first partition estimations for each team. Data partitioning is crucial, as disregarding the origin of estimations could result in less accurate estimations. Different teams can have very different ways of working, resulting in disparate estimations.

Additionally, automatic estimation tools should also consider whether teams are working on multiple projects. Tasks created for different projects may have a very different set of requirements. If the tool is retrieving data from an Agile project management tool, such as Jira, different projects could be identified with tags. This would then be taken into consideration by the prediction model to improve the accuracy of predictions. 

As a stretch, estimation tools could also target predictions for different epics. Each epic may deal with a different part of a system, which presents a different set of challenges. Naturally, a model cannot be trained on an epic that has no estimated tasks. In such cases, it could use the data from the remaining project at first, and refine it once tasks for the epic are estimated. This would allow predictions to become more accurate once more tasks are estimated.

These approaches will not be as accurate when there is little data for given a team or project. In such cases, an automatic estimation tool should still be able to use data from past project. This should allow the model to still be useful in the first development stages when data is not as refined.  

## Final thoughts
The process of estimating Agile tasks requires a considerable amount of time and is very subjective. Additionally, it is a process that is prone to errors and that sometimes requires the re-estimation of tasks.
Having a model capable of automatically estimating Agile tasks would not only provide significant time savings, but also decrease subjectivity by basing predictions on previous estimations. Nonetheless, automatic task estimations seem to come with some downsides. Given the complexity of modern applications, it becomes increasingly hard for a model to automatically estimate tasks.

An additional concern must be made about the training of such estimation models. Given all estimations are ultimately done by humans, a model can only be as good as the data it is backed by. If the aim is to achieve a high prediction accuracy, tasks must be updated with their real estimations when requirements change. 

Lastly, it is crucial to reduce the scope of the dataset to only make predictions based on relevant estimations. Estimation data should be gathered for each team, as there may be different perspectives on how to classify work. Furthermore, mixing data from multiple projects can lead to inacuracies. Different projects can have different dependencies and (most likely) a completely different structure and architecture, which fundamentally changes the way they are developed.
Naturally, this will reduce the amount of data the model can be trained on, but could arguably prove advantageous in removing prediction outliers.

## Sources
- [Using Statistics for Agile Estimations](https://github.com/mlarionov/machine_learning_POC/blob/52cdece108f285a4e67212fd289f6dbf9035dca0/agile_estimation/agile_estimation_2.ipynb)
- [Lean Forecasting in Software Projects](https://repositorio-aberto.up.pt/bitstream/10216/128576/2/412448.pdf)
- [An Ensemble-Based Framework to Estimate Software Project Effort](https://www.sciencedirect.com/science/article/abs/pii/S0164121222002187)
