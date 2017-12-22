# Status
Rejected, probably? I submitted 2 proposals through LISA17's early CFP system, where they would give feedback and encourage you to re-submit for the regular CFP. I ended up having my other proposal accepted to LISA17, so I did not re-submit this talk. I got some useful feedback that leads me to believe this would have been rejected, though. (And also I submitted it to so many other conferences that rejected it!)

# Submission Title
DIY Network Tracing When All You Have is Python

# Talk or Tutorial?
Talk or Panel

# Duration of Talk or Panel
30 minutes including Q&A

# Topic Category
_LISA has three broad categories for submissions: Architecture, Culture, and Engineering. See the CFP for more information_

Engineering

# Specific Topics
_Information on what your submission will specifically cover, for example "Load Balancing, Capacity Planning" or "Mentorship, Team Culture"_

Monitoring, distributed tracing

# Audience Takeaways
_What do you expect the audience to take away from your submission? If a tutorial, What will they bring back to work?_

The audience should come away with a practical understanding of how they can instrument their Python backend to collect data about network activity without relying on complex open source systems. I will be going through these details with enough detail that people could implement the ideas themselves.

The technical details are tangential to a broader lesson about being empowered with the understanding that we can get a great deal of insight from just a little bit of Python. If I had to pick a Pixar movie to represent my talk's lesson, it would be Ratatouille: Anyone can do infra. You learn about cooking in Ratatouille, but it's not the main point. The main point is that you can have a huge impact even with a humble beginning. I plan to get this message across explicitly, but also implicitly by sharing my background as a new grad with little networking experience prior to starting this project.

# Submission Abstract
_Here it is, your chance to submit an abstract! Describe your submission, give outlines, any useful information that we can use to help us review your submission. This is what we'll put on the website to describe your talk if accepted. Corrections can be made later._

_PLEASE: leave out any identifying information! Abstracts that list names or specific titles will be edited by the organizing committee before review._

Abstract:
In monitoring, we start with a simple question, "What's going on in my system?", and quickly get overwhelmed by an avalanche of open source libraries and SaaS vendors promising to answer all of our questions in neat packages. We want the answers, but we feel paralyzed by the complexity of setting up instrumentation, the uncertainty of investing months of time without guaranteed benefit, and the fear that generic tools might not fit our specific situations.

In this talk, I'll share the motivation behind why we wanted to pursue network tracing and how we implemented a barebones tracer with a fraction of the development time. I'll talk about why we decided to build our own simple tracer before embarking on a year-long journey to get Zipkin into our system. I'll go into the details of how just a little bit of Python and a big DIY attitude helped us empowered to tackle big problems and cut down our latency by over 20%.

Outline:
SECTION: Introduction
About my background, my company, and what my team does.

SECTION: Problem statement
I will explain the problem/solution I mentioned in my description: Why did we think network tracing would benefit us and how did we plan to do it without going to an existing tool like Zipkin or Stack Driver?

We have dozens of API endpoints that are making requests to our backend services, but no individual engineer knows how many requests are made by an endpoint and how much time it spends on each request. We had a suspicion that there were many network calls that were unnecessary (e.g., requesting data that had already been requested, requesting data in series instead of in parallel), but we didn't know how to find those requests. We also have many types of network calls from which a request can be made, for example, memcache, thrift, redis, http, s3, and others. If we used a tool like Zipkin, we risked missing an entire category of network calls. How could we make sure we were capturing a complete picture of our codebase?

SECTION: Solution
Definitions:
Socket module - The socket module is Python's interface with the operating system's networking system calls. Because it is the lowest level networking module that all other networking modules (e.g., urllib, requests) are built off of, we knew that any call to any of these backends would eventually have to call the socket module.

Monkey patching - We monkey patched the socket module to record all network calls. Monkey patching means that we swapped out the socket module with our own version of socket at runtime. My patch did exactly the same thing as the original socket, but would record every call before executing.

Putting it all together:
We monkey patched the socket module and now we know what that means. How do we enable it in our code? I'll talk about how we used decorators to turn on a flag to say "monitor this function", stored the data in our telemetry system (statsd and OpenTSDB), and visualized our results for other engineers.

SECTION: Conclusions / Wrap up
Outcomes:
I'll quickly talk about what we gained from the project. We had a 25% improvement in latency on our homepage and search results. We also finally added Zipkin to our system, but it took nearly a year and several engineers to implement, in contrast to the two months it took me (new grad at the time!) to implement this monkey patch project.

Takeaways:
- Every engineer should feel empowered to do big things no matter where they think their experience level is.
- The scrappy, DIY mindset is one way to get through paralysis from being overwhelmed by tools.
