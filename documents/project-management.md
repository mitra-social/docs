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

- It's not the goal to implement the complete ActivityPub standard in this master thesis. Additional functions should be implemented after the master thesis, as there is just not enough time for a complete implementation of the ActivityPub standard.

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
- **MA-02** The ActivityPub standard implementation on our side should be as complete as possible for the implemented use-cases so we can cover all variations of requests/responses. We need to check the major other ActicityPub projects and test if they behave according to the standard and if not maybe implement some fallbacks by compromising the proper implementation of the standard on our side as less as possible. **But first of all make sure that non-conform server instances don't break our application.**

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
