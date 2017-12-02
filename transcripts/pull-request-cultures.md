# Pull request cultures I've participated in

Open source or company codebase

## Commenting on pull requests

### Who reviews?

- everyone
- for some parts of code, you want reviews from specific people before merging
	- ping these people in the PR when opening it

### What goes in a review?

- "that's not how we do things" cultural coding norms
	- ideally shouldn't include stylistic formatting stuff, autoformat rules should take care of that
- "this code is difficult for me to understand" - for when you find yourself reading a section of code over and over, and are having trouble tracking exactly what it's doing.  It might just be something you don't know yet, but probably needs to be simplified in code, or improved with more accurate function/variable/class names
- "is this business logic accurate" - state what you think the code is doing, and ask for clarification that it's what we want the code to do.  If you misunderstood what the code was doing, the code needs to be made more obvious.  If the business logic is wrong, that gets fixed before merging.  It might be worthwhile to add a comment saying why that business logic is being used.
- No personal comments.  Talk about the code only.  Assume good faith.

### What communication is okay outside of official comments on the pull request?

This is controversial.  Many people believe that all communication should happen through pull request comments, so that there is a history of what was talked about, and other people on the team can see what was discussed, so they don't re-comment on things, and can learn from anything that was brought up.

Comments on the pull request should be the general case, but I do prefer to take some things to direct message chat.

Some kinds of long questions about fuzzy or high-level topics are difficult to answer in comments without making personal defenses.  This happens because these pull request comments are written in big atomic blocks, and also because they happen in public.  You have to write long paragraphs to explain yourself fully, and doing it in front of everyone makes you want to defend your choices when you're talking about more subjective topics.

Especially in the cases where I want to have a discussion about something to see where someone was coming from, but I don't have a very strong opinion or I want to give them a chance to convince me in a back-and-forth manner, I will go to direct messages.

If I want to figure out, say, what pattern we want to use for batch database jobs in the future, it's easier to set up a conversation where we can collaborate and bounce ideas back and forth in a direct message than in a pull request comment where they'll feel pressured to write a long defense of their implementation in that commit against my vague questioning.

## Who merges?

I've worked with either one of:

- approved people merge at some point after things are reviewed
	- could be enforced by Github permissions, or by cultural convention
- the person who opened the review

Open source projects with liberal contribution models like Rod Vagg's ["OPEN open source"](https://changelog.com/rfc/7) model seem to usually wait for the person who opened the PR to merge.
