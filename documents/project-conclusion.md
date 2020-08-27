# Project completion

## What has been achieved

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

## What was not achieved

Use cases with low priority have been postponed.

In more detail:

- "Automatic update of the post feed from the frontend. (Due to low priority.)
- "Deleting a user" is not yet implemented. (Due to low priority.)
- "Forgot password" has not yet been implemented. (Due to low priority.)
- Retrieving an outbox (on demand or within a certain interval) of a remote actor was considered obsolete and will not be implemented.

## Conclusion

The application can be used as an activity feed. (External) users can be looked up and followed. The followed users can be filtered. The user can make a minimum of adjustments to his profile. (Namely email and password.)

The challenge was to understand and implement the ActivityPub standard.
The ActivityPub standard was not implemented so carefully by other servers and presented us with certain problems. Specific adjustments to other implementations must be made at a later point in time to raise compatibility with other servers.

The stabilization of the backend side took way more time than expected. Since more incoming data from different servers brought more and more content problems to light. Most common incompatbilities could be remedied. Additionally caching was a big topic as well to improve read performance. Especially what and how to cache.

In the front end, the time waster were the unit tests. Because the know-how was not on a very high standard. Nevertheless, a test coverage of over 95% was achieved. And in the end it was an instructive part.

During the development process it became clear that it makes sense to be able to follow other users in as many ways as possible. Search new actors via webfinger id or follow them through the activity feed.

The highlight was when the application could communicate with other servers for the first time and users on our server were able to follow actors on remote servers and receive their activities in the feed.

The structure of the backend and frontend is prepared, so that the write access can easily be incorporated at a later point in time and a switch to asynchronous messaging is possible.
