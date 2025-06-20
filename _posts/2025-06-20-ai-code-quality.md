---
layout: post_with_comments
title:  "Balancing Speed and Quality: AI’s Impact on Software Development"
date:   2025-06-20 18:00:00 +0000
categories: blog
---

In just a few years, artificial intelligence has gone from a curiosity to an essential part of the modern developer's workflow. With the recent rise of AI tools such as Cursor, we've seen a number of developers now relying on these tools to complete tasks from start to finish. Since AI tools have become particularly effective at coding, it makes sense that we're witnessing this increase in adoption. Driven by the promise of increased productivity, companies have further accelerated this trend. 

There's been an overwhelming adoption of all sorts of AI tools. What initially began with a simple text-based prompt has evolved into a fully integrated coding environment capable of handling all but the most complex tasks—sometimes without the developer writing a single line of code. As a result, the role of the developer is being refocused, highlighting the architectural and strategic thinking that has always set great developers apart. Developers are now primarily responsible for designing the system or task, while the computer takes on the role of materializing those ideas into code that can be compiled by the machine.

This shift in how we build software raises an important question: what happens to the process of shaping and reshaping code over time? One of my biggest concerns is that we may begin to lose the ability to iteratively evolve our implementations. Concepts like premature optimization may start to fade from discussion, as AI tools can now generate "perfect" solutions from the start. The notion of procedural, iterative development is being replaced by a system that delivers answers upfront, leaving less room for exploration or gradual refinement.

I'm not an AI expert—just a software developer with a perspective. But as someone who cares deeply about how we build and maintain software, I've been thinking a lot about what this means for the craft of development. This isn't a critique of AI. In many ways, these tools are powerful, impressive, and genuinely helpful. But they're also changing the way we think about our work as developers and how we collaborate with our tools.

In the rest of this article, I want to reflect on a few of those changes: how AI affects things like refactoring, how we evaluate productivity, and how it might reshape the role of the developer itself. These aren't definitive answers, just thoughts on a rapidly evolving landscape that's redefining what it means to write code.

## Refactoring in the Age of AI: What the Data Reveals

I have a strong sense of order, and when my code feels out of place, I tend to incrementally rewrite it to match my mental model before adding any new features. This aligns closely with Martin Fowler's definition of refactoring: code should evolve incrementally, as small changes are easier to reason about and review. While AI tools are increasingly capable of refactoring code, they often generate large blocks of it without necessarily grasping the full context of the codebase. Tools like Cursor have made impressive strides in this area, and I've seen promising results when asking cursor to refactor my code. After all, AI performs well in environments governed by well-defined rules, and refactoring is a discipline that has been around for a long time. But can it do well in the long run? 

To get a clearer picture, it's worth looking at some concrete data that highlights how development practices are already starting to shift. The latest GitClear report for 2024 highlights intriguing trends around how codebases are evolving in the AI era.

One of the standout findings concerns the volume of code being added to repositories. Since AI tools became widespread, the total lines of code (LOC) have been steadily increasing. AI simply makes it easier than ever to generate more code quickly. According to GitClear, LOC has grown about 2–3% YoY since 2020 (before AI's rise), with a sharper increase starting in 2023.

But perhaps even more revealing than the volume of new code is what's happening with moved lines of code. These are lines that are relocated within the codebase as part of refactoring and reorganization. Moving code is a positive indicator, reflecting developers' efforts to improve structure and reduce duplication. Unfortunately, this metric has been steadily declining since 2020, falling from roughly 25% of changed lines being moved to under 10% in 2025.

Given how AI tools typically operate, ffocusing on generating new code rather than reorganizing existing code, this decline makes sense. And in my view, this is the most concerning insight: development has shifted from a multi-step process that includes reshaping and refining code, to one that centers almost entirely on new implementation. We're moving from sculpting our codebases to building on top of them.

Maintaining a codebase takes time and continuous effort from developers to avoid pitfalls like technical debt. While AI tools can significantly speed up development, it remains to be seen whether they can also help keep our codebases healthy in the long run. Adding code is one thing. But maintaining it is a far more complex and involved task. Perhaps what we need is a defined set of standards and rules that AI tools can use to perform code reviews before implementing new features.

Codebases are already challenging to maintain. The larger they grow, the more cumbersome development becomes. Martin Fowler shares a story in his book "Refactoring" about a company overwhelmed by technical debt. Despite his advice to refactor and clean up their code, leadership decided to ignored him, focusing instead on rapid feature delivery. Over time, the growing technical debt slowed development and hurt product quality, eventually leading the company to shut down. is story highlights the critical importance of regular refactoring and maintaining a healthy codebase, not just for developer sanity, but for the survival of the business itself.

All of this raises a broader concern. It isnot just about how we write and maintain code, but how we evaluate it. If the development process is changing, our tools for measuring it should change too. That brings me to another topic that AI has pushed to the front of my mind: metrics.


## A New Look at Code Metrics
One of the things AI has really made me reconsider is how we measure productivity in software development. Metrics have always played a central role, especially for managers who need some kind of quantitative signal to track progress or evaluate performance. There's a saying: "What gets measured gets improved". But in the context of AI-assisted coding, I think we need to be especially careful. Goodhart's Law comes to mind: "When a measure becomes a target, it ceases to be a good measure". If people have always found ways to game metrics, AI has only made it easier.

Take lines of code (LOC), for example. It's historically been used as a measurement for productivity. But in today's reality, where I can ask an AI tool to refactor a large chunk of my code or expand a function and instantly generate hundreds of lines of code, LOC has lost what little value it had as an indicator of meaningful contribution. It's no longer a sign of progress, it's just a number that's trivially inflated.

In my opinion, we need to drastically rethink how we measure developer output. Instead of looking at raw quantity, we should shift toward evaluating the quality and impact of contributions. In practice, this is difficult to evaluate, but perhaps it's also an opportunity to leverage AI for smarter code analysis. A simpler approach could be to start identifying and rewarding signs of thoughtful engineering: reduced duplication, modular structure, clear abstractions, and so on.

Moving code, for example, shouldn't count toward raw output, but it's often a subtle indicator of refactoring and reorganization. It deserves to be acknowledged - not as a number to inflate performance reviews, but as a sign of care and long-term thinking.

Perhaps in the near future, developer review sheets will include not just bugs fixed or features shipped, but metrics like duplicated lines removed, files reorganized, or complexity reduced. These may be less flashy, but they speak volumes about the health and sustainability of a codebase.

## Beyond Automation: Rethinking the Role of the Developer

As AI tools become more capable, it's easy to start thinking of them as replacements for human effort. After all, they can generate entire components, write tests, refactor legacy code, and even suggest architectural changes. But in practice, the developer's role isn't disappearing: it's evolving.

AI is very good at certain tasks: repetition, pattern recognition, applying rules at scale. It can sift through massive codebases and generate solutions quickly. But that speed and scale come with a catch: AI doesn't understand the project. It doesn't know why decisions were made, how edge cases are handled, or what trade-offs exist in a given context. That context still lives with the developer.

In a recent podcast titled The Rise of Cursor, Michael Truell, co-founder and CEO of Anysphere (the company behind Cursor), makes a striking observation: the way we interact with code, and with computers more broadly, is on the verge of a fundamental change. He predicts that programming will move beyond traditional code to natural language or pseudocode, making software development more accessible to non-coders. On the other hand, profesionals would still be able to have the required development precision and make necessary adjustments.

This vision aligns with emerging tools like SuperWhisperer, which allow developers to simply speak their intentions to the computer. The computer becomes less of a tool we manually command and more of a communication interface. It is becomign more of a collaborator that translates natural language into functioning software.

If we embrace this new vision, then maybe we should stop asking, "Can AI replace developers?" and start asking, "How do we design workflows where developers and AI can complement each other?" In this model, AI becomes a powerful assistant, not a replacement. One that can offer suggestions, take care of boilerplate, and even handle tedious refactors, while the developer remains in charge of the big picture.

## Conclusion
AI is undeniably transforming the landscape of software development. It's transforming not just our approach to development, but also making us rethink how we measure productivity. While these tools bring incredible power and efficiency, they also challenge longstanding practices like refactoring and thoughtful code maintenance. The data suggests we may be trading attention to detail for speed and volume, raising important questions about the sustainability of this new approach.

However, it also redefines developers as orchestrators and curators who guide AI's output using their context and judgment. This also suggests that we can use AI to our advantage. By defining the right set of rules, we can improve how we measure productivity. But it's equally important to make sure we're measuring the right things.

Ultimately, the future of development will depend on how we blend our skills with what AI has to offer. Embracing that balance may be the key to not just faster code, but better code and better software.