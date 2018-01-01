# Status
Rejected

# Title
DIY Performance Tuning When All You Have is Python?!?

# Abstract
My team needed to figure out where our API endpoints were spending all of their time. We knew about open source tools like Zipkin, but we didn't want to invest months of work on implementing it without a clear payoff. So we did the next best thing: we rolled our sleeves up, used our understanding of Python and networking, and wrote our own simple tracer. With just a little bit of Python and a big DIY attitude, I'll show how an understanding of programming fundamentals can help us feel empowered to tackle overwhelming problems.

# Timeline
(3 minutes) Introduction to problem:
We have dozens API endpoints each calling our backend services. We don't know immediately from reading the code which calls are being made, whether those calls are sequential or parallel, or whether they're returning unnecessary data. We could either scrap the entire product and start from scratch ("this time we won't make any inefficient calls!"), or we could work with what we have and eliminate the problems ("I didn't realize I was calling the database twice!"). This is where network tracing comes in handy: we can monitor the network calls our code makes and use this data to identify bad calls.

(5 minutes) But how!?
In Python, you can do this thing called monkey patching. You completely replace a module with a module of your own (ideally one that implements the same interface as the original module). Once you swap the original module with your "patched module," all subsequent code will use the patched module without being aware that it was changed. We patched the socket module because it's the lowest level foundation of all network calls in Python and so we were guaranteed to catch calls from all types of tools that use network calls (e.g., urllib, redis). Our patched socket sneakily records data about each network call and then calls the original socket module. Wherever we wanted to collect data, we decorated our code to say "start tracing only in this section." With this data, we could see when rogue network calls were being made.

(2 minutes) You can do this too!
This was my first project at $myCompany and we managed to cut down our latency by 20% because of this project. I had never taken a networking class and I had only used Python for simple scripts in the past. This project taught me that anyone can do systems programming. It's not always an esoteric journey into kernel programming or anything scary. It's just finding a problem, thinking about how the tools we already have can fix those problems, and diving in.

# Intended audience
Two groups: junior engineers and infra people. I mostly want to share this with junior engineers to spread the message of "you can do impactful things even if you're inexperienced!" I keep thinking of my favorite Pixar movie, Ratatouille: anyone can cook! No matter your background, anyone can pick these concepts up and use them to make big contributions.

Infra/monitoring/SRE people will also benefit from my talk because I'll discuss the implementation with enough detail that they could probably go home and implement the same ideas in their own codebases.

