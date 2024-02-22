---
layout: post_with_comments
title:  "Task Estimation"
date:   2024-02-22 20:10:00 +0000
categories: blog
---

After reading some articles on the subject of automatic Agile estimations, I was left with the feeling that no matter the estimation strategy, we were never going to get around the main issue at hand: The human factor. Despite all the recent research done on the topic, replacing experts for task estimation has proven to be a hard problem to solve. Being able to automatically estimate tasks requires tremendous knowledge of, at least, the state of the existing codebase, deployment and testing environments, and external dependencies. This is ignoring other factors, such as availability, seniority, and knowledge of the code base, just to name a few. In an ideal world, we would have a development environment with no fluctuations in work scope and a history of very accurate task predictions. Naturally, this is something that is hardly achievable, as work scope varies drastically (either because of unpredicted side-effects or unforeseen dependencies to an ongoing task) and task estimation can only go so far, as it relies on the knowledge available during planning. Real world conditions may affect this initial prediction and affect the initially planed scope.

Having said all that, it might seem like I am a pessimist and don't see this topic advancing so much in the next years. That is definitely not the case (trust me!), but I do believe some boundaries have to be established when moving forward wit automatic Agile estimation. Without any particular order, here are my thoughts on it.


## Tackling Unknowns
The first aspect to consider when trying to estimate Agile tasks is to define known unknowns and unknown unknowns. This might sound confusing at first, so let me try to explain it briefly. 

When you are creating a task, there will be key requirements necessary to complete it that you are aware of, but don't yet know all the details for. These will be your known unknowns. To identify how you will tackle these requirements, you perform your investigation and define a what you need to complete the task successfully. As an example, consider you are creating a task to implement a new API endpoint. The endpoint will be used to retrieve a list of historic Gas Prices stored in an existing database. In your investigation, you discovered what protocol is the most appropriate, how to validate incoming data properly, what level of security is required, and so on.
After successfully creating your task, you add it to the backlog and it is now ready to be estimated. When your team goes to the planning, they all have a look at it and throw their estimations. When all are happy and have reached the final estimate, you consider that the task is ready for development and call it a day. It is as simple as that!

Some time has past, and the task you've created a week earlier was added to the next sprint and is now being actively developed by someone from your team. However, that developer discovers an issue with the endpoint that is being developed. In your initial proposal, you suggested returning a list with all the Gas prices the system had stored. However, because your system has been storing this data for some time now, retrieving all of them in a single request has proven to be a problem, causing your endpoint to time out each time someone attempted to call it. After re-evaluating your initial implementation, you imediately come to the conclusion you require pagination. So you update your initial set of requirements and have the developer adjust the endpoint to consider this new requirement. 

This second aspect is called an unknown unknown. This had sliped through when you were developing the endpoint, as you were unaware of the fact that the system was storing so much data and had no data retention policy. Such things can happen and will require you to likely re-evaluate your initial estimate. 

Coming back to the story of automatic task estimations, it is such details that make task so hard to predict. In this case, our developer accidentally left out an important part of an endpoint's design. 


## Sources
- [Agile Estimation using Monte Carlo](https://link.springer.com/chapter/10.1007/978-3-540-68255-4_17)