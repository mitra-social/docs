## Project

### What has been achieved

At the end of the project an application was achieved with that you can follow other users, read posts and filter posts by user. It features a simple design and is easy to use.

In more detail:

- Compliant to the ActivityPub standard.
- A user can register and log in. Logging out works on the front end side.
- The user can change their email and password in their settings
- Follow and unfollow other users was the only write access planned to be implemented and is successfully implemented.
- The incoming activities are processed in the backend and enriched with the corresponding "in reply to" activity and user information.
- Images can be displayed as thumbnail in post and displayed in full size in a dialog.
- The post can be filtered by a user. When paging the posts, the filter is retained until the filter is deactivated.
- Searching for users with the web finger id works. Some information about the searched user is also displayed in the search dialog.

### What was not achieved

Use cases with low priority have been postponed.

In more detail:

- "Automatic update of the post feed from the frontend. (Due to low priority.)
- "Deleting a user" is not yet implemented. (Due to low priority.)
- "Forgot password" has not yet been implemented. (Due to low priority.)
- Retrieving an outbox (on demand or within a certain interval) of a remote actor was considered obsolete and will not be implemented.

### Conclusion

The application can be used as an activity feed. (External) users can be looked up and followed. The followed users can be filtered. The user can make a minimum of adjustments to his profile. (Namely email and password.)

The challenge was to understand and implement the ActivityPub standard.
The ActivityPub standard was not implemented so carefully by other servers and presented us with certain problems. Specific adjustments to other implementations must be made at a later point in time to raise compatibility with other servers.

The stabilization of the backend side took way more time than expected. Since more incoming data from different servers brought more and more content problems to light. Most common incompatbilities could be remedied. Additionally caching was a big topic as well to improve read performance. Especially what and how to cache.

In the front end, the time waster were the unit tests. Because the know-how was not on a very high standard. Nevertheless, a test coverage of over 95% was achieved. And in the end it was an instructive part.

During the development process it became clear that it makes sense to be able to follow other users in as many ways as possible. Search new actors via webfinger id or follow them through the activity feed.

The highlight was when the application could communicate with other servers for the first time and users on our server were able to follow actors on remote servers and receive their activities in the feed.

The structure of the backend and frontend is prepared, so that the write access can easily be incorporated at a later point in time and a switch to asynchronous messaging is possible.


## Franco

The work was exciting. The highlight was receiving posts from other applications where activitypub also implemented standards. Working with Pascal was great. I was able to learn a lot from him and the communication between us worked well.
I mainly work on the frontend. Vuejs turned out to be a good framework. The longer the project took, the more the benefits of Vuejs became apparent. With vuetify you had a library with good standard components that could appear in an application. The front end can be started with mock data or a backend can be specified where the data is called.
I am satisfied with the result. There are some points that I would do differently now than at the beginning. Of course it still has some bugs. Unfortunately the time passed in flight to fix further bugs or to improve the display.

### Positive conclusion

- The display of the post that has been replied to.
- The search for new users is well implemented.
- Simple design
- Mock Date and Unit test

### Negative conclusion

- The data from the server / mock are processed in different components instead of centrally in the store.
- That the application is not yet mobile enough
- Understanding ActivitPub was very challenging.

### What did I learn from the project

- Got to know Vuejs extensively
- Write a test
- Set up the front end via Docker
- That I have to get better at reviewing


## Pascal

It was a very exciting and interesting project. The longer I worked on this project the more I realized that our world wide web as we know it as of today became way to 
centralized and that we definitely should break things up again. The huge centralized services make the world wide web attractive to hackers, risky for our privacy and 
vulnerable against outages. Breaking everything up into small services run by many private people or as well small companies where the compatibility between these services
is guaranteed through open standards could bring us back the www we all loved back in the days.
Developing decentralized applications however is rather complex and many shortcuts are not possible we normally would do in a centralized service.

### Positive conclusion
- I see the power in decentralized web solutions
- I'm super happy that we were able to release a version that is almost fully integrated into the Fediverse and can communicate with other servers.
- The excitement I felt through the whole master thesis as I knew when I solved on problem, the next challenge was just around to corner waiting to be solved.
- I loved to work together with Franco. We really had the same mindset and our skills added up to each other very well.

### Negative conclusion
- Implementing a standard can be very frustrating as it's 100% sure that if 3 people implement a rather complex standard there will be incompatibilities between all 3 implementations.
- I spent way too much time debugging incompatible servers to find out what's going wrong with our requests. And I spent way too much time implementing work arounds.
- We couldn't achieve to create a standalone libraty to publish and consume with the ActivityPub standard as we were to busy integrating the planned features.
- GitHub projects is still in a very early stage and barely suitable for iterative project management. I definitely would use Jira over GitHub projects.
- Working in sprints and planning them is difficult if the working hours per sprint vary heavily.

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
