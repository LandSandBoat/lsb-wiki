**Not yet live**

## Headers
I am using...
- [ ] Windows
- [ ] Linux

I want to...
- [ ] Play solo on the same machine I host on
- [ ] Play just on my own home network (no internet players)
- [ ] Run a public server (on the internet)
- [ ] Run a public server (on the internet) for many people

I want to host...
- [ ] On my machine
- [ ] On a different machine
- [ ] On a cloud-based instance

## Introductory Content
- Get the prerequisites
- Set up the database
- Modify my configuration
- Build the server
- Configure my network (port forwarding etc.)
- Running the server

## Basic Content
- Logging
- Monitoring
- Guide to GM-ing

## Advanced Content
- Client version support
- Maintenance
- Upgrades
- Automation
- Performance
- Large-scale hosting

## Large-scale hosting
**TODO: Collect more information from servers** 

_A lot of these notes are anecdotal, but they come from successful servers hosting large amounts of players (**up to 1000 concurrent**), and from people who have been in the community a long time._

The game server is _essentially_ single-threaded. So on its own, it isn't able to utilize more than a thread or two. Rather than trying to re-architect the entire application to be multithreaded and introduce all of the awful and hard-to-debug problems that come with multithreaded design, it was decided that it would use interprocess-communication (IPC). IPC allows multiple processes to be spun up and for them to communicate through a central messaging system. The library we use for this is [ZeroMQ](https://zeromq.org/):

> ZeroMQ (also known as ØMQ, 0MQ, or zmq) looks like an embeddable networking library but acts like a concurrency framework. It gives you sockets that carry atomic messages across various transports like in-process, inter-process, TCP, and multicast. You can connect sockets N-to-N with patterns like fan-out, pub-sub, task distribution, and request-reply. It's fast enough to be the fabric for clustered products. Its asynchronous I/O model gives you scalable multicore applications, built as asynchronous message-processing tasks. It has a score of language APIs and runs on most operating systems.

#### Note
It has been observed many times that multiple map processes straight up don't work when split different machines (or split across multiple VMs). This setup results in a slew of difficult to diagnose problems and strangeness in your zones. If you want to scale to more concurrent players, you need to upgrade to a more powerful machine.