# Concurrency

One *major* issue I have identified whilst working through the design of the questionaire is managing *concurrent writes to the datastore*.

If two users arrive at the same leaf node—prompting them to submit a question of their own—which one gets written to the datastore? Which one is associated with the leaf node? How is this conflict resolved?

After answering a series of questions I expect a user to spend some time deliberating over their own question. This is a major problem since it would require leaf nodes to be ‘locked’ for long periods of time. Subsequent users would have to wait for a pending question to be submitted before they could proceed—making for a very unfavourable experience.

As the tree grows, the likelihood of this scenario will likely dwindle as more leaf nodes emerge. However, when the tree is in its infancy this issue will be prevalent.

## Solutions

I have considered a number of options to address this problem:

1. Allow for multiple questions to be associated with the same leaf node.
	- Users arriving at a node with multiple questions attached to it would be served one at random.
	- **CON:** This would immediately invalidate the binary structure of the data and the nature of the project.
	- **CON:** Users taking the questionaire a second time might be served different questions—an idea I am not happy with. **I want journeys through the tree to be seeded by impulsive honesty. I want them to be repeatable.**
2. The data structure and questions could remain completely detached.
	- **PRO:** The data structure could remain a binary tree.
	- **CON:** Incrementing a node's yes/no counters regardless of the question that was answered removes any correlation between the questions and the data structure. In such case the tree structure might as well be automated.
3. Create orphan questions that are attached to random leaf nodes if their ‘destination’ node is consumed by another question.
	- **PRO:** Users arriving at a leaf node can take as long as they like to submit a question.
	- **PRO:** Having the question submission at the end of a journey serves as a reward whilst also offering inspiration.
	- **CON:** Randomly located questions bear no correlation to a participants journey through a tree.
4. Questions are precomposed.
	- Rather than formulating and submitting a question at the end of a journey through the tree, questions are composed before starting the questionaire and immediately attached to a leaf node when one is reached.
	- **PRO:** This would reduce the ’lockdown time‘ of a node significantly.
	- **PRO:** Questions are not influenced by any preceeding questions that the user would have answered.

> I want journeys through the tree to be seeded by impulsive honesty. I want them to be repeatable.

## Direction

I feel that the best user journey follows the flow of answering a series of questions and then asking one. Asking a question at the end of the journey is both rewarding and logical—to me anyway.

Subsequently, I have decided to persue **Solution No.3**. User submitted questions will be attached to their destination leaf node if available, otherwise it will be temporarily orphaned and reattached to another leaf node.

To maintain a degree of correlation between the user's journey and the location of their question, orphaned questions will be allocated to the closest available leaf node on an emanating branch upstream from their destination.

