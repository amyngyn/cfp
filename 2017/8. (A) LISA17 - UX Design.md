# Status
Accepted. I submitted this through LISA17's early CFP system! I was really grateful to see that there was a way for an inexperienced/new speaker to improve their chances of acceptance and that was a big factor in why I submitted anything at all.

# Submission Title
UX Design and Education for Intuitive Monitoring Tools

# Talk or Tutorial?
Talk or Panel

# Duration of Talk or Panel
30 minutes including Q&A

# Topic Category
_LISA has three broad categories for submissions: Architecture, Culture, and Engineering. See the CFP for more information_

Engineering

# Specific Topics
_Information on what your submission will specifically cover, for example "Load Balancing, Capacity Planning" or "Mentorship, Team Culture"_

Training, education, UI/UX design, monitoring

# Audience Takeaways
_What do you expect the audience to take away from your submission? If a tutorial, What will they bring back to work?_

Motivational and theoretical lessons:
- The biggest impact you can have as a monitoring engineer is by improving the UX of your internal tools and educating the rest of the engineers in your company. You can be a 10x engineer by making 10 other engineers work faster.
- Design your tools for laypeople - don't assume domain-specific knowledge. Imagine your hypothetical customer as someone who hasn't used any telemetry/logging systems yet (more common than you think) and check your assumptions about what people should know when using your tools.

Actionable lessons (Education):
- Know when it's time for education vs intuition: Sometimes it's important that a user understands distinctions about their metrics (e.g., don't use the average of percentiles), but most of the time it's not important (e.g., is their data coming from Graphite or OpenTSDB?).
- Clear, updated, and discoverable documentation is a part of the user experience of interacting with your team. In our case, we found it best to write a single page of all common questions with a table of contents so that users could cmd+F the topics they were interested in and skim. This was an improvement over our previous system of adding a new wiki page of instructions for every question.
- Make yourself open and accessible - if your team is intimidating or unfriendly to newcomers, people will struggle silently rather than asking you questions.

Actionable lessons (UX):
- Reduce friction by anticipating the most common use cases and pre-fill those as defaults in your tool
- Lessen anxiety by rewarding users for exploration. For example, if a user refreshes a page or clicks the back button, they shouldn't lose their progress; if they are looking at the configuration for something, they shouldn't be afraid of accidentally making an irreversible change.

# Submission Abstract
_Here it is, your chance to submit an abstract! Describe your submission, give outlines, any useful information that we can use to help us review your submission. This is what we'll put on the website to describe your talk if accepted. Corrections can be made later._

_PLEASE: leave out any identifying information! Abstracts that list names or specific titles will be edited by the organizing committee before review._	

The fastest way to become a 10X engineer is by enabling 10 other engineers to do their jobs better. As infrastructure engineers, a huge amount of our work is about empowering the rest of our engineering organizations to use the tools we develop correctly, quickly, and effectively. Yet we spend so much time explaining how to interpret timeseries data and why averaging percentiles is a bad idea. How can we make this experience better for everyone?

After receiving feedback from our teammates, we embarked on a journey to redesign our internal monitoring tools and understand where people were struggling with the existing system. In this talk, I will explain how we approached the problem of making concepts like interpolation, aggregation, and alerting more intuitive and how we identified pain points for new users. I'll go over common misconceptions our users have about monitoring and how we cleared up this confusion with improved training and UI design. By the end, you will be able to critique and improve the user experience of your internal tools.
--
I don't have an outline to provide for this talk (yet), but I plan to discuss the three broad areas I covered in the "Audience Takeaways" section in roughly the same order.

---

# Modified after acceptance / before conference

# Description
The fastest way to become a 10X engineer is by enabling 10 other engineers to do their jobs better. As infrastructure engineers, part of our mission is to empower the rest of our engineering organization to use the tools we develop correctly, quickly, and independently. Yet we often fall short of that mission in unexpected ways. In this talk, I will explain ways to make concepts like interpolation, aggregation, and alerting more intuitive and how to identify pain points for new users. I'll go over common misconceptions users have about monitoring and how you can clear up this confusion with improved training and UI design.

# Bio
Amy Nguyen is a software engineer passionate about making data understandable for everyone. In the past, she studied computer science and philosophy at Stanford University, served on the board of Stanford Women in Computer Science for three years, and helped in making computer science the most popular major for female undergraduates during her time there. Outside of work, Amy writes about the tech industry, loves baking, and reads too many self-improvement books.

# Title
UX Design and Education for Effective Monitoring Tools
