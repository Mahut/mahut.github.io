---
layout: post
title: Context Switching and Task Interruptions
comments: true
tags: [developer, productivity, context switching, multitasking]
---

_As a professional developer, I often get some deeply focused sessions of work, especially when I’m programming. One thing I’ve noticed is the difficulty to resume after I get interrupted from those sessions. My role also requires me to be involved in more than one project, thus jumping from one task to another not necessarily related. It’s hard, without a strategy to quickly get back into an interrupted work in progress._

This difficulty has been studied and explained by cognitive scientists and psychologists. It’s called _context switching_. In this post I share their findings and my comprehension of the subject and give some strategies to reduce the impact of the inevitable.


## Computers vs Humans

It all started with the word _multitask_, invented by IBM in 1985 to describe a computer capability. 

A multitask operating system is designed to work on multiple tasks but not at the same time. It works briefly on the first task, then saves the system state for that task. The interrupted task moves to the end of the queue and the system switches to the next task until all the assigned tasks are considered done. This operation is so fast that we have the impression that all the tasks are executed at the same time. The process of storing the state in order to pause the task and resume another is called context switch. A context switch can also occur as the result of an [interrupt](https://en.wikipedia.org/wiki/Interrupt).

We can find similarities between how computers multitask and how humans "multitask". For humans, multitasking means [trying to perform two or more tasks concurrently, which typically leads to repeatedly switching between tasks (i.e., task switching) or leaving one task unfinished in order to do another.](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7075496/)


## What is Context Switching ?

Context switching, also called task switching, is to jump from one task to another unrelated task, causing a mental shift resetting the working memory. Context switching is a consequence of multitasking. 

It happens when for example you’re writing an email to explain an issue and get interrupted for a support task by instant messaging. Or when you’re writing technical documentation and paused for a code review. 


## What causes Context Switching?

Context switching can be caused by something as simple as self interruptions (not motivated to pursue the task on hand, boredom, need to take a break etc.). Other triggers are external events like a shoulder tap, a question from a colleague or a simple disruption like a notification.

For developers, it can be a pull request which interrupts a programming task or multiple upcoming unrelated meetings. Unforeseen events related to ongoing projects can also be sources of context switching (changes in a task priority, blockages due to unavailable resources etc.).

And last but not least, there's the myth that multitasking makes us overachievers, efficient and high performers. Our contemporary work culture values and rewards multi-taskers and responsiveness and our digital tools don't help.

No wonder that at the end of the day most of us feel exhausted and drained.


## The Cost of Context Switching 

As you may have guessed, context switching has a cost (as for [computers](https://en.wikipedia.org/wiki/Context_switch)). We may think that we’re getting more done by accepting more and more tasks and by switching between them but it’s counterproductive. The American Psychological Association (APA) found in a [study](https://www.apa.org/topics/research/multitasking) that it leads to a 40% decrease of an employee's productive time.

Context switching impacts our mental energy, our brain and even our memory. Even your IQ can be impacted. A [study by the University of London](http://discovery.ucl.ac.uk/1465496/) found a decrease in IQ for participants who multitasked during complex cognitive tasks.

Another study conducted by Gloria Mark, a Professor from University of California Irvine found that [it takes up to 23 minutes to refocus our effort after just one interruption](https://www.fastcompany.com/944128/worker-interrupted-cost-task-switching). This leads to more stress, working faster to get more done, thus makes us superficial thinkers.

To study the effects on developers in more detail, [Chris Parnin and his colleagues](https://link.springer.com/article/10.1007/s11219-010-9104-9) made an exploratory analysis of 10000 programming sessions recorded from 86 programmers using Eclipse and Visual Studio, and a survey of 414 programmers. They found that a programmer takes between 10-15 minutes to start editing code after resuming work from an interruption. It’s less than the 23 minutes mentioned earlier but no less important. Also, when interrupted during an edit of a method, only 10% of times did a programmer resume work in less than a minute. And finally, developers only get one uninterrupted 2-hours session per day.

It seems context switching cannot be totally avoided. Especially in modern software development, when you’re part of a team and involved in agile projects. But how can we manage to reduce its impact?


## How to reduce the Impact of Context Switching?

On the developer’s desk, there are a few things to do in order to reduce context switching. It’s important to have a "where was I?" strategy in case of interruptions. What I found helpful is to quickly jot down keywords linked to the context of the interrupted task. It reduces the load on my working memory and the time it takes to resume the task. It’s also good to adopt best practices in development like clean code (clearly named variables, methods, classes, well organised code, etc.). That way, the code itself can help resume the programming session. 

Some IDEs like Eclipse have a set of tools to improve resumption of development tasks.One of those plugins is [Mylyn](https://www.eclipse.org/mylyn/). It integrates various task trackers such as Bugzilla, Mantis, JIRA. 

When you mark that you are working on a given task, Mylyn activates the context including the various files opened during analysis and development.

On a more macro level, it’s important to work on how your day is scheduled. For example, you can batch together linked tasks, meetings. Our common advice is also to schedule the more important tasks first in the morning or at the end of the day. The thing here is to have a dedicated, not interruptible period of time. It’s also important to learn how to prioritise. You can ask your manager for help if needed. 

If your role requires responsiveness, you need to figure out what level of responsiveness you need to provide. You can also adopt asynchronous communication. When balanced with synchronous communication, It can improve the developing experience and leads to more quality responses.


## Conclusion

In this post I’ve tried to give more insights on context switching and task interruptions and how they impact knowledge workers, especially developers. Psychologists have studied context switching, and found it can negatively impact our productivity and also our mental health in many ways... However it’s important to note that not all interruptions are a big loss. Switching tasks is unavoidable and sometimes can even increase developers productivity in some cases. In fact it all depends on the context in which it occurs. If a colleague working on the same project as you interrupts to exchange ideas about the task at hand this can be a productive interruption.
