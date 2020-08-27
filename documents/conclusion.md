## Project retrospective



## Franco

### Positive conclusion

### Negative conclusion

### What did I learn from the project



## Pascal

It was a very exciting and interesting project. The longer I worked on this project the more I realized that our world wide web as we know it as of today became way to 
centralized and that we definitely should break things up again. The huge centralized services make the world wide web attractive to hackers, risky for our privacy and 
vulnerable against outages. Breaking everything up into small services run by many private people or as well small companies where the compatibility between these services
is guaranteed through open standards could bring us back the www we all loved back in the days.
Developing decentralized applications however is rather complex and many shortcuts are not possible we normally would do in a centralized service.

### Positive conclusion
* I see the power in decentralized web solutions
* I'm super happy that we were able to release a version that is almost fully integrated into the Fediverse and can communicate with other servers.
* The excitement I felt through the whole master thesis as I knew when I solved on problem, the next challenge was just around to corner waiting to be solved.
* I loved to work together with Franco. We really had the same mindset and our skills added up to each other very well.

### Negative conclusion
* Implementing a standard can be very frustrating as it's 100% sure that if 3 people implement a rather complex standard there will be incompatibilities between all 3 implementations.
* I spent way too much time debugging incompatible servers to find out what's going wrong with our requests. And I spent way too much time implementing work arounds.
* We couldn't achieve to create a standalone libraty to publish and consume with the ActivityPub standard as we were to busy integrating the planned features.

### What did I learn from the project
I learnt about reactive programming in PHP. Especially the limited resources on Heroku challenged me quite a lot. I had to come up with a solution for an easy to
use process forking mechanism in PHP to run multiple processes as the whole appliaction needs at least 2 independent processes to communicate with external servers
properly and don't end up in a deadlock. Of course I could have just spinned up another instance of our application but this would have brought us into the non-free
tiers of Heroku as another Dyno would have been necessary. The way I solved it in the end, we can share/save resources and still have multiple processes running in
just one free Dyno of Heroku. I learnt quite some fundamentals about AWS and especially their S3 services when I had to look for a caching solution for media files,
as well as about the abstraction of the file system in a cloud native application. 
I also learnt quite some stuff about messaging and message buses.
Last but not least I learnt, how a flexible, uncensorable and decentralized network needs to be designed, how it works and that it definitely is the future for 
social networks. Taking away the power from single companies and bring the power back to the actual users of the network. And I learnt a lot about challenges and 
principles of decentralized applications and about the design of standards.
