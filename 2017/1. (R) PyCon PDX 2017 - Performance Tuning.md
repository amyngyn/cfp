# Status
Rejected

# Title
DIY Performance Tuning When All You Have is Python

# Duration
I prefer a 30 minute slot

# Description
In monitoring, we start with a simple question, "What's going on in my system?", and quickly get overwhelmed by an avalanche of open source libraries and SaaS vendors promising to answer all of our questions in neat packages. We want the answers, but we feel paralyzed by the complexity of setting up instrumentation, the uncertainty of investing months of time without guaranteed benefit, and the fear that generic tools might not fit our specific situations.

In this talk, I'll share my first experience writing production-quality Python as a new software engineer to solve a problem we had been stuck on for years. We wanted to know where our backend was spending its time and where we could make it faster. We knew it would take months to get an open source tool like Zipkin to work in our system, so we instead used our understanding of networking and Python to find a solution that met most of our needs with a fraction of the development time. With a little monkey patching and a big DIY attitude, we'll learn to feel empowered to tackle problems with Python on our side.

# Who and Why (Audience)
This talk is mainly for beginners who are interested in learning how Python can be relevant to infrastructure and site reliability engineering. I plan to explain the main Python and networking concepts relevant to my problem at a high level. These include monkey patching and the socket module, but will not cover much more networking than that. Essentially, the audience will understand that data is sent and received through sockets, but I won't say much more about networking than that. The audience should already be familiar with using Python classes and decorators, but I will quickly explain it for the unfamiliar.

I'll be discussing a realistic problem that engineers could go home and implement in their own systems, so I expect devops/SRE folks to be interested in this talk as well. Still, I believe the technical details are tangential to a broader lesson about being empowered with the understanding that we can get a great deal of insight from just a little bit of Python. If I had to pick a Pixar movie to represent my talk's lesson, it would be Ratatouille: Anyone can do systems. You learn about cooking in Ratatouille, but it's not the main point. I plan to get this message across explicitly, but also implicitly by sharing my background as a new grad with little networking experience prior to starting this project.

# Outline
SECTION: Introduction / About Me (2 minutes total)
(2 min) Background - My current job is my first job out of college and I've been working there for about two years. I work on making monitoring tools accessible for everyone, which means that I make sure our tools are up and fast for debugging incidents, make sure that the user experience is good, and make sure people are well-educated on what their data means so they can make informed decisions. I'll say a longer version of this with the intention of emphasizing that monitoring is a field that ties together design, UX/UI, systems, and front end. (I have a secret agenda of making infrastructure less intimidating and more multifaceted, which is why I want to dedicate a few minutes to explaining my job.)

SECTION: General problem with deciding between open source / in house / paid solutions (6 minutes total)
(3 min) The open source vs paid vs in house debate - I will go over the benefits and costs of choosing open source versus paid solutions versus in-house solutions. I think that for more seasoned engineers, this debate is somewhat tired, but I want to cover the big points for beginners who haven't heard this debate yet. The big points will be:
- Paid solutions don't allow for customization and might not be mature enough to accomplish what you want, but can save you development time and maintenance.
- Open source solutions might not fit into your architecture, but you can get support from the community and contribute code changes.
- In house development will let you move quickly, but you don't get to fully leverage the expertise of others who have been down this path before. You also (usually) won't be contributing your work back to the community.

(3 min) Decision paralysis and needing to move forward - In my description, I wrote, "We want the answers, but we feel paralyzed by the complexity of setting up instrumentation, the uncertainty of investing months of time without guaranteed benefit, and the fear that generic tools might not fit our specific situations."

I will talk about these three concerns and the problem of paralysis when it comes to fields with big open source communities (like monitoring, but also common in JS community, for example). I'll talk about how it feels as a beginner to enter a field, hear that I need to know about OpenTSDB, Graphite, Grafana, Redis, etc, and to read all of the documentation in order to be productive.

SECTION: Technical problem statement (3 minutes total)
(3 min) I will explain the problem/solution I shared in my description: "We wanted to know where our backend was spending its time and where we could make it faster."

We have dozens of API endpoints that are making requests to our backend services, but no individual engineer knows how many requests are made by an endpoint and how much time it spends on each request. We had a suspicion that there were many network calls that were unnecessary (e.g., requesting data that had already been requested, requesting data in series instead of in parallel), but we didn't know how to find those requests. We also have many layers of network calls from which a request can be made, for example, memcache, thrift, redis, http, s3, and others. If we used a tool like Zipkin, we could miss an entire category of network calls. How could we make sure we were capturing a complete picture of our codebase?

SECTION: Technical solution (10 minutes)
(2 min) Socket module - The socket module is Python's interface with the operating system's networking system calls. Because it is the lowest level networking module that all other networking modules (e.g., urllib, requests) are built off of, we knew that any call to any of these backends would eventually reach the socket module.

(4 min) Monkey patching - We monkey patched the socket module to record all network calls. Monkey patching means that we swapped out the socket module with our own version of socket at runtime. My patch did exactly the same thing as the original socket, but would record every call before executing.

(3 min) Putting it all together - We monkey patched the socket module and now we know what that means. How do we enable it in our code? I'll talk about how we used decorators to turn on a flag to say "monitor this function", stored the data, and presented our results to engineers.

(1 min) Outcomes - I'll quickly talk about what we gained from the project. We had a 25% improvement in latency on our home page and search results. We also finally added Zipkin to our system, but it took nearly a year and several engineers to implement, in contrast to the two months it took me (new grad!) to implement Pinpoint.

SECTION: Wrapping up (9 minutes)
(2 min) Restate the debate from the introduction - One of the points of my talk will be that going "in-house" doesn't necessarily mean that you can't go open source later on. I want to talk a little bit about how the debate isn't as rigid as "open source vs paid vs in-house", but about what's right in your specific context. In our case, we eventually ended up using Zipkin and it took us nearly a year to get it working. But that doesn't mean that the Python code that I wrote was a waste of time - it actually proved to us that tracing was a valuable thing to do and laid the foundation for going with open source later on. I also want to complicate the idea that open source is best and that everything should be written with the intention of eventually open sourcing. In our case, we needed something very specific to our system and Zipkin didn't fit it (without a year of work).

(2 min) Summary of lessons
- Every engineer should feel empowered to do big things no matter where they think their experience level is.
- The scrappy, DIY mindset is one way to get through paralysis from being overwhelmed by tools.

(5 min) Q&A

# Additional notes
This will be my first time giving a talk. I plan to give this talk at local meetups before PyCon.

In terms of public speaking experience, I spent three years in college teaching discussion sections for introductory computer science and am comfortable with pacing a 50 minute class and explaining technical concepts to beginners.

Regarding subject matter experience, I wrote all of the code that I will be discussing in this talk. I will have worked in monitoring for nearly 2 years by the time of the conference.

	•	Have a concrete question in mind
	•	Have a technical solution planned out

