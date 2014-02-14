# Data Collection

![Questionaire Concepts](../project_images/2014-02-13-10.43.31.jpg)
*—designing the node data structure and questionaire interface*

## Questions & Hypotheses

* Will users engage with the experiment?
* Will they understand it?
* Will they feel lost or get bored if the sequence of questions gets too long?
* Will the tree reach a critical size?
* Will users be more interested in answering questions or asking one of their own?

Assuming that the experiment gets any traffic at all, I predict that the tree will quickly reach a critical size where participants get bored of answering questions and leave.
Subsequently I expect the initial yes/no counters towards the root of the tree to increment fairly consistently. Longer branches will likely suffer from greater falloffs towards their leaf nodes.
If this is not addressed, the submission of questions will suffer and the data structure will stagnate.

As a potential solution, each tree could have a lifecycle dictated by either time (one day for example) or a condition such as:

* Maximum branch length: A new tree is created when a chain of nodes reaches a critical length.
* Falloff threshold: A new tree is created when the number of users leaving the experiment exceeds a limit.
* Root node traffic volume: A new tree is created when the number of users answering the root node question exceeds a limit.

## Technologies & Approach

Google App Engine will be used for the backend—providing both a datastore and API which the front–end can interact with.
Angular.js will be used on the front–end to update the interface as the participant traverses through the questionaire.
Google Analytics will be employed to track user interaction with the application.
