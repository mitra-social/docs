# Project Mitra

## Project period

| Project start | End of project |
| ------------- | -------------- |
| 2019-09-26    | 2020-08-28     |

## Project goals

An application has to be developed that is capable of the following functions:

- A potential user is able to register and then log in with the newly created user.
- A user should receive posts from other users they're following.
- Contemporary and simple design.
- Easy handling - ActivityPub for the masses.

## Justification, benefits

- Many implementations of the Standard ActivityPub are clones from well-known social media platforms, we want to get the best stuff of them all.
- Reduce the limitations of how to implement the ActivityPub standard.

## Non-goals

- Additional functions should be implemented after the master thesis, as there is not enough time for a comprehensive implementation of the ActivityPub standard.

## Criteria for the successful end of the project

- A working installation where a logged in user can see posts.
- Documentation completed.

## Necessary core project team

- Software Engineer
- PHP Developer
- Javascript Developer

## Risk analysis

### Risks

#### Project

- **RP-01** Unknown protocol ActivityPub - No project member has ever worked with this protocol so the risk is that it takes us a long time to successfully manage it or don't manage to get it working at all.
- **RP-02** Scope - The project of building a social network server based upon the ActivityPub standard is a huge endeavor therefor the risk is given that the scope is not defined well or even not defined at all.

#### Application

- **RA-01** Slow third parties - Due to the decentralized approach of the project there is the possbility that remote servers are responding very slow or not at all.
- **RA-02** None-standard conform third parties - Due to the decentralized approach of the project and various implementations of the protocol on different servers there is the possibility that server instances not always behave the same and don't implement the ActivityPub standard properly which could lead to bugs and missing information in our application.

| Risk No. | Impact   | Likelihood |
| -------- | -------- | ---------- |
| RP-01    | **high** | _small_    |
| RP-02    | medium   | medium     |
| RA-01    | **high** | **high**   |
| RA-02    | _small_  | **high**   |

### Measures

#### Project

- **MP-01** Plan enough time and resources in the beginning to understand the standard well and do some prototypes/proof of concepts.
- **MP-02** Clearly define the scope (see for example the use-cases we want to cover within this project)

#### Application

- **MA-01** Calls to third parties should be made asynchronously to prevent slow response times on our implementation.
- **MA-02** The ActivityPub standard implementation on our side should be as complete as possible for the implemented use-cases so we can cover all variations of requests/responses. We need to check the major other ActicityPub projects and test if they behave according to the standard and if not maybe implement some fallbacks by compromising the proper implementation of the standard on our side as less as possible. Additionally make sure that non-conform server instances don't break our application.

## Milestones

![Timeline Gantchart](./stuff/project-mitra-timeline.jpg)

- **green:** done
- **blue:** open
- **orange:** not implemented

## Meetings

### Monthly with project members and mentor
- [05.03.2020](./minutes/2020-03-05.md)
- [02.04.2020](./minutes/2020-04-02.md)
- [17.04.2020](./minutes/2020-04-17.md)
- [30.04.2020](./minutes/2020-04-30.md)
- [28.05.2020](./minutes/2020-05-28.md)
- [25.06.2020](./minutes/2020-06-25.md)
- [13.08.2020](./minutes/2020-08-13.md)

## Project completion

### What has been achieved
At the end of the project an application was achieved with that you can follow other users, read posts and filter posts by user. A simple design and it's easy to use.

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
