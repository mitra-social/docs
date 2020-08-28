# Architecture & Design

## Backend

### Block view level 1

![architecture-block view level 1](./diagrams/architecture-block-view-level-1.svg)

- **API:** The API reflects the service with its endpoints as described in the ActivityPub standard (for example: inbox/outbox/user endpoints) plus some additional endpoints not discussed in ActivityPub standard document but necessary for the proper functioning of the application (for example: register/token issue endpoint). In general the API component MUST be implemented non-blocking in regard of calls to remote servers. Thus all calls to remote servers MUST be reflected by tasks pushed into the _**Queue**_ and handled asynchronously. This guarantees fast response times for the API. Although there MAY be some exceptions like pulling a remote user's outbox explicitly by a call to a dedicated endpoint for this.
- **Worker:** The worker processes the tasks in the _**Queue**_ and executes all the calls to external servers to push or pull information requested in the currently processed task. The worker MAY push follow up tasks into the _**Queue**_.
- **Queue:** The queue holds all the open tasks that need to be processed by the _**Worker**_ component.
- **DB:** The database component in general stores all the information generated on the server through either the _**API**_ or _**Worker**_ as well as external fetched content through the _**Worker**_ component.
- **File system:** All media data like images, videos, etc. either produced through API calls or through calls to remote servers by the _**Worker**_ is stored in the file system and references to the location are stored in the _**DB**_.

### Class diagram

![Class diagram](./diagrams/class-diagram.svg)

### Message bus - write into inbox

![message bus write into inbox](./diagrams/message-bus_write-into-inbox.png)

This shows the commands and events dispatched if an activity hits the inbox endpoint of a user.

* ASContentReceivedEvent: An incoming ActivityPub activity hit the user's inbox (contains the DTO)
* AttributeContentCommand: Assign an "author" to the incoming activity
* ContentAttributedEvent: An author has been assigned to the activity
* ValidateContentCommand: Check the valid format of the incoming activity 
* ContentRejectedEvent: The content is not validated successfully
* ContentAcceptedEvent: The content has been successfully validated
* UpdateExternalActorCommand: If the activity is of type `Actor` the corresponding actor gets updated in the local database.
* ExternalUserUpdateEvent: The external user has been updated successfully in the local database.
* PersistContentCommand: Store the activity in the local database
* ContentPersistedEvent: The activity has been stored in the local database successfully
* DereferenceCommand: Dereferences possible related activities (e.g. `inReplyTo`)
* DereferenceEvent: Additional activity has been dereferenced
* AssignContentCommand: Assign the activity to the subscribed internal user
* ContentAssignedEvent: The activity has been subscribed successfully to the internal user

## Frontend

### Block view level 1

![architecture-frontend block view level 1](./diagrams/architecture-frontend-block-view-level-1.svg)

- **Router** — All the routes of the project (in our case we store them in the index.js). In Vue.js everything is a component. But not everything is a page. A page has a route like “/dashboard”, “/settings” or “/search”. If a component has a route it is routed.
- **Components** — All the components of the project that are not the main views
- **Views** — To make the project faster to read we separated the components that are routed and put them in this folder. The components that are routed are for us more than just a component. Since they represent pages and they have routes, we put them in “views” so when you want to check a page you go to this folder.
- **Store** — The Vuex constants in mutation-type.js, the Vuex modules in the subfolder modules (which are then loaded in the index.js).
- **API-Client** — API client is a service for calling up data. An HTTP request is sent to the backend server or directly to the Fediverse. It is also possible to configure a mock server.

### Process description

#### Block view level 1 - Get posts

![process-descriptions-fetch posts block view level 1](./diagrams/process-descriptions_fetch-posts–block-view-level-1.svg)

**Login**

- 1.0 The user logged in.
- 1.1 The frontend gets the latest posts from the backend and prepares it for viewing.
- 1.2 The user can view the posts.

**Scroll**

- 2.0 The user scrolls down.
- 2.1 The frontend gets the next newest posts.
- 2.2 The user can view the posts.

**Pulling posts**

- 3.0 After a defined time, the latest post is triggered in the frontend.
- 3.1 The frontend gets the latest posts from the backend and prepares it for viewing.
- 3.2 The user can view the posts.

### Block view level 2 - Get posts: Login

![process descriptions-login fetch posts-block view level 2](./diagrams/process-descriptions_login-fetch–posts_block-view-level-2.svg)

- 1.0 The user logs in with their credentials on the login page.

- 2.0 The router directs the user to their home page with the posts.

- 3.0 The components let the lifecycle `created` run.
- 3.1 In the `created` function, the `fetchCollection()` is called from the _CollectionStore_.
- 3.2 `getPost()` is triggered as soon as the items in the _collectionStore_ are updated.

- 4.0 The _collectionStore_ calls the _apiServer_ to receive the collection data.
- 4.1 If the data comes back from the _apiServer_, the collection data is saved in the _collectionStore_
- 4.2 If a collection item is a create, it is checked whether the object is one of the post types and pulls the post out and adds it to the list of posts.
- 4.3 If a collection item is an update, it is checked whether the object is one of the post types and pulls the post out and adds it to the list of posts and deletes the old post from the list.
- 4.4 If a collection item is a delete, the ID is read out and filtered out of the post list.

- 5.0 Backend gets request of the inbox of the user for the latest posts.

### Activity Diagramm

#### Pull out actor's display name

##### Version 1

![pull out actors add name 1](./diagrams/pull-out-actors-add-name-1.svg)

- 1.0 The actor property (`actor` or `attributedTo`) is extracted from the activity object and passed to a Util method that extracts the display name from the object.
- 2.0 It is checked if the object has the property _name_ and that it is not empty.
  - 2.1 If yes, the content is returned from the object by the property _name_.
- 3.0 It is checked if the object has the property _namemap_ and that it is not empty.
  - 3.1 If yes, the language is fetched from the browser. In the future multilanguage should be possible and the language should be taken from the user's settings.
  - 3.2 With the language input, the corresponding name is extracted from the object. If the language does not exist, the first value in the _namemap_ object is taken ([must still be fixed on issue 36](https://github.com/mitra-social/mitra-frontend/issues/36)).
- 4.0 It is checked if the object has the property _preferredUsername_ and that it is not empty.
  - 4.1 If yes, the content is returned from the object by the property _preferredUsername_.
- 5.0 It is checked if the object is an URL (string). If not, default _undefined_ is returned.
  - 5.1 First it is checked whether the URL has already been called to prevent an infinity loop. If this has already been the case and is still an URL, _undefined_ will be returned.
  - 5.2 With the URL, a call is made to the Fediverse to get the actor information. Then the method for extracting the name will be run again and marked that the method has already been run.
- 6.0 If none of the conditions apply, _undefined_ will be returned.
- 7.0 Finally, the name is displayed in the component.

##### Version 2

- 1.0 The actor property(`actor` or `attributedTo`) is read from the activity object's response from the backend.
- 2.0 It will be checked if it is an URL. If it is not, continue with 5.0.
- 3.0 A call is made to the Fediverse with the URL in order to receive information about the actor.
- 4.0 The `actor` property's activity object is overwritten with the information from the Fediverse.
- 5.0 The status of the data from the store is updated with the data from the response of the backend.
- 6.0 The affected components update the data from the store and thus the display of the name has to be updated again with the method of Util to extract the display name.

- 7.0 It is checked if the object has the property _name_ and that it is not empty.
  - 7.1 If yes, the content is returned from the object's _name_ property.
- 8.0 It is checked if the object has the property _namemap_ and that it is not empty. 
  - 8.1 If yes, the language is fetched from the browser. In the future multilanguage should be possible and the language should be taken from the user's settings.
  - 8.2 With the language input, the corresponding name is extracted from the object. If the language does not exist, the first value in the _namemap_ object is taken ([must still be fixed on issue 36](https://github.com/mitra-social/mitra-frontend/issues/36)).
- 9.0 It is checked if the object has the property _preferredUsername_ and that it is not empty.
  - 9.1 If yes, the content is returned from the object by the property _preferredUsername_.
- 10.0 It is checked if the object has the property _id_ and that it is not empty.
  - 10.1 If yes, the content is returned from the object by the property _id_.
- 11.0 It is checked if the object is an URL (string).
  - 11.1 If yes, the URL will be returned
- 12.0 If none of the conditions apply, _undefined_ will be returned.
- 13.0 Finally, the name is displayed in the component.

![pull out actors add name 2](./diagrams/pull-out-actors-add-name-2.svg)

##### Decision

The first version had the disadvantage that the call to the external server was in the util method and the _dump_ components had additional tasks because of the asynchronous call.
In the second version, the various data are put together correctly in the store and therefore the util method does not have an additional asynchrony and the _dump_ components do not need any additional logic.

#### Search actor with their followers and following list

![process description search actor](./diagrams/process-description_search-actor.svg)

- 1.0 User enters the web finger ID of the user they are looking for and click on the search button.
- 1.1 The search result is reset when the dialog is closed.
- 2.0 `searchActor` is a wrapper function for the store's `findActor`. The error handling of the action is handled in the wrapper.
- 2.1 The actor is returned when the `user` state has been updated.
- 2.2 The follower list is returned when the `followerCollectionPage` state has been updated.
- 2.3 The following list is returned when the `followingCollectionPage` state has been updated.
- 2.4 Reset user search data.
- 3.0 This function calls the API to fetch the user basic information in the Fedivers with the web finger. The Fediverse object contains an URL where you can request the detailed data of the user, if the user exists. This URL is called. The actor's detailed information is set in on return. The actions for followers and following lists are called with the URL, which contains the detailed information of the actor.
- 3.1 Calls the API for the web finger. The web finger id is given.
- 3.2 Calls the API for a collection. The follower URL is given to the API. The collection is set to the follower state and paging is set for this collection.
- 3.3 Calls the API for a collection. The following URL is given to the API. The collection is set to the following state and paging is set for this collection.
- 3.4 The status of the find-user store gets resetted.
- 4.0 Calls the web finger with the GET in the Fedivers using the web finger id entered by the user and return URL of searched user.
- 4.1 Calls up the user information with the GET in Fedivers with the URL that comes from the web finger and returns a user.
- 4.2 Calls the collection with a URL with the GET in Fedivers. An ordered collection page is returned.
- 4.3 Calls the collection with a URL with the GET in Fedivers. An ordered collection page is returned.
