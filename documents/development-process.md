# Development process
## Flow
1. [Idea 💡](https://github.com/mitra-social/mitra-docs/issues?q=is%3Aissue+label%3A%22idea+%F0%9F%92%A1%22): In the very beginning there's an idea about a feature, improvement, etc.
2. [User story 📓](https://github.com/mitra-social/mitra-docs/issues?q=is%3Aissue+label%3A%22user+story+%F0%9F%93%93%22): If the idea from step one gets evaluated and seems to be duable as well as important to do it becomes a user story. 
3. Grooming: The user stories get groomed and estimated. There are technical and non-technical discussion/clarifications and maybe some refinements of the user story taking place during the grooming.
4. Selecting for development: User stories that fulfill the definition of ready (DoR) eventually get assigned to a sprint.
5. If a user story is assigned to sprint it will be either pulled into the [Project Board](https://github.com/orgs/mitra-social/projects/2) as soon as the sprint starts or rescheduled.
6. Optionally technical tasks get created for frontend and backend and linked back to the user story and added to the [Development Project Board](https://github.com/orgs/mitra-social/projects/1).
7. Development: Necessary code gets developed and tested through integration and/or unit tests.
8. A Pull Request gets opened against the `master` branch.
9. Changes get reviewed by another developer.
10. As soon as the new code passes code style, static analaysis and the tests pass (ensured by CI) it can be merged into `master` branch.
11. For the backend repository the `master` branch gets automatically deployed to the staging enviornmen on Heroku (https://mitra-social.herokuapp.com)  once there are new changes merged into it. There's no automated deployment of the frontend repository yet.
12. Requirements get verified by the owner of the user story.

## CI
Powered by Travis CI: https://travis-ci.org/github/mitra-social

* Backend: https://travis-ci.org/github/mitra-social/mitra-backend
* Frontend: https://travis-ci.org/github/mitra-social/mitra-frontend

## CD
Once there are changes merged into `master`branch they automatically get deployed by Heroku (for both, frontend and backend):

* Backend: https://mitra-social.herokuapp.com
* Frontend: https://mitra-social-frontend.herokuapp.com

## Definition of Ready (DoR)
- User story is groomed and reviewed by developers from core team
- User story is estimated
- User story contains at least one acceptance criteria

## Definition of Done (DoD)
- User story is completely implemented
- The main flow are tested through integration and/or unit tests
- Newly written code passes static analysis and code style check
- Code has been reviewed and approved by another member of the core team
- Open PRs are merged into `master` branch
