---
layout: post_with_comments
title:  "Three Days with AI: Build Fast, Fix it Later"
date:   2025-08-25 16:00:00 +0000
categories: blog
---

I suppose it was inevitable. At some point I had to try building something with AI. Not just to see what all the fuss was about, but also to understand the limitations of the tools that companies are so eager to adopt in the name of productivity. With one Cursor license in my pocket, and with Anthropic offering users the chance to try GPT 5, I decided it was the perfect moment to put it to the test. 

So I decided to challenge myself: write as little code as possible and let AI help me create an app I had been wanting for a long time: an app to track my expenses while traveling. Over the course of just three days, not even full ones, I managed to put together a fully functional expense tracker. That still surprises me. A project like this would normally take much longer, especially when balancing both backend and frontend work. But with GPT 5 as my co-pilot, the process felt less like traditional coding and more like orchestrating.

The app itself wasn’t just a toy project. It could take a natural language input like *“Add two flights at 1500 each to my Japan trip”* and break it down into structured data: category, type, quantity, unit price, and total. It also supported manual entry through a form, so users could fall back to traditional input when needed. Beyond that, it included the ability to split those expenses among members. And because any app like this needs at least some form of identity management, I added basic authentication with registration and login.

For three short days of development, it was more than I expected: a complete proof of concept, functional, usable, and ready to demo. But the real story lies in the process itself. So in this short post I want to share my experience using Cursor, mostly with GPT 5, and reflect on what it got right and where it fell short.

For those curious to check out the code it produced, the code is available on [GitHub](https://github.com/MiguelMarcelino/divvyup).

### The Challenges of Building with AI

Getting to a working prototype so quickly felt exciting, but the process was far from effortless. Along the way I ran into several obstacles that revealed some of the shortcomings of building with AI. Some of these challenges were small annoyances, while others pointed to deeper limitations in how these tools approach coding.

One of the first patterns I noticed when working with AI was its tendency to repeat itself. And this aligns with [GitClear's 2025 code quality report](https://www.gitclear.com/ai_assistant_code_quality_2025_research), which highlights similar issues in AI generated code. GPT-5 would sometimes generate nearly identical blocks of code across different parts of the project. This left me with duplication I had to refactor. In a way, though, it was a blessing in disguise: I used the same AI to clean up the codebase, guiding it toward better abstractions. Still, it made me realize that "clean" isn’t its default. It requires careful direction.

Another issue I ran into was pagination. When I asked the AI to implement it, the solution it offered was to slice the list on the frontend while still fetching *all* the entries from the database. This was one of the cases where it completely missed the underlying purpose: reducing the amount of data fetched from the Database. It also highlighted a recurring pattern: AI tends to optimize for something that works rather than something that scales. If I hadn’t been keeping a close eye on the AI, I would have ended up with a problem that might only have surfaced months later, once the backend was already in full use.

This was the overall pattern with backend code: a lack of attention to optimization. GPT-5 reliably produced working solutions, but almost never the most efficient ones. Whether it was database queries, caching, or handling larger datasets, the AI rarely anticipated performance concerns. Unless I explicitly asked for optimization, it defaulted to the simplest path.

Switching gears to the frontend, describing layouts was its own kind of learning curve. Saying "place this next to that" or "align this element with that section" often led to odd placements or messy styling. Over time, I figured out that being highly precise with my instructions was key. The AI did eventually give me the layouts I wanted, but it required practice in communicating clearly what I envisioned.

Some challenges cut across both the frontend and backend. At times, the AI would produce code that simply didn’t work, and it would only correct itself after compiling the project and reading the output. It often felt like trial and error, rather than a reliable process, which didn’t inspire a lot of confidence. You couldn’t always trust that what the AI gave you would run correctly on the first try.

I'd say the most important risk I want to highlight with all these examples is the overreliance on AI. If I hadn’t carefully reviewed the code it produced, I would have ended up with mistakes or inefficient implementations that could have caused bigger problems down the line. AI can accelerate development, but it doesn’t understand context, trade-offs, or long-term maintainability. A developer still needs to guide, review, and validate everything. Otherwise, that extra speed provided by AI will come at the cost of quality and tech debt.

### The Positives

Despite those limitations, I would still say the overall experience was positive. The biggest benefit was speed. Normally, scaffolding an application like this would take days by itself. With GPT-5, I was able to describe requirements and see them implemented within minutes.

That speed made it possible to quickly iterate and get to a working prototype without being bogged down in boilerplate or setup. Within three days, I had something tangible I could put in front of people. Not a diagram, not a mock-up, but a real application. That kind of acceleration is invaluable for proof-of-concepts.

It was also cost-effective. Most of the coding was done with GPT-5 through Cursor, and the iteration cycle was not only fast but also inexpensive compared to the time and resources it would normally take to build a similar prototype. For showing ideas, gathering feedback, and experimenting with features, it was nearly perfect.

### Reflections on the Role of the Developer

Looking back on those three days, what stands out most is how different the process felt compared to traditional development. I wasn’t buried in syntax or spending hours wiring up basic features. Instead, I was guiding, refining, and correcting. The AI gave me *a* solution, but rarely *the* right solution. My role was to provide the context, the trade-offs, and the long-term thinking.

That distinction matters. AI doesn’t understand *why* certain decisions are made. It doesn’t know what technical debt means in the context of a growing project, or how performance trade-offs might affect scaling later. What it does know is how to quickly produce functional code, and that’s powerful. But only when paired with human judgment.

For me, this project was a glimpse of where software development is heading. Developers won’t disappear, but their role will continue to evolve. Less typing, more directing. Less about syntax, more about strategy. The AI handles the boilerplate and the obvious, while we focus on the bigger picture.

### Concluding Thoughts
Three days was all it took to build an app that, not long ago, would have taken me much longer to piece together. GPT 5 took care of the mechanics of coding, while I supplied the intent and the judgment to steer it in the right direction.

The result was far from perfect. It worked as a proof of concept, but it would not survive untouched in production. That gap is where the real problem with AI shows itself. These tools are excellent at speed, but speed alone is not enough. Working code is not the same as reliable code, and without careful review, the shortcuts AI takes today can easily turn into technical debt tomorrow.

If this is what I can build in three days with AI, the possibilities of what we can achieve in weeks or months are staggering. But we should not mistake acceleration for progress. To get the most out of AI, we need to pair its speed with human oversight, context, and long-term thinking. The true power of these tools only emerges when they are guided responsibly, with developers staying firmly in the loop.

