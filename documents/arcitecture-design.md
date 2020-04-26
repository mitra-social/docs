# Architecture & Design

## Backend

### Block view level 1

![Class diagram](./diagrams/architecture-block-view-level-1.svg)

- **API:** The API reflects the service with its endpoints as described in the ActivityPub standard (for example: inbox/outbox/user endpoints) plus some additional endpoints not discussed in ActivityPub standard document but necessary for the proper functioning of the application (for example: register/token issue endpoint). In general the API component MUST be implemented non-blocking in regard of calls to remote servers. Thus all calls to remote servers MUST be reflected by tasks pushed into the _**Queue**_ and handled asynchronously. This guarantees fast response times for the API. Although there MAY be some exceptions like pulling a remote user's outbox explicitly by a call to a dedicated endpoint for this.
- **Worker:** The worker processes the tasks in the _**Queue**_ and executes all the calls to external servers to push or pull information requested in the currently processed task. The worker MAY push follow up tasks into the _**Queue**_.
- **Queue:** The queue holds all the open tasks that need to be processed by the _**Worker**_ component.
- **DB:** The database component in general stores all the information generated on the server through either the _**API**_ or _**Worker**_ as well as external fetched content through the _**Worker**_ component.
- **File system:** All media data like images, videos, etc. either produced through API calls or through calls to remote servers by the _**Worker**_ is stored in the file system and references to the location are stored in the _**DB**_.

### Class diagram

![Class diagram](./diagrams/class-diagram.svg)

## Frontend

### Class diagramm

#### Block view level 1

![Class diagram](./diagrams/architecture-frontend-block-view-level-1.svg)

- \**Router*3 — All the routes of your projects (in my case I have them in the index.js). Basically in Vue.js everything is a component. But not everything is a page. A page has a route like “/dashboard”, “/settings” or “/search”. If a component has a route it is routed.
- **Components** — All the components of the projects that are not the main views
- **Views** — To make the project faster to read I separate the components that are routed and put them in this folder. The components that are routed for me are more than a component since they represent pages and they have routes, I put them in “views” then when you check a page you go to this folder.
- **Store** — The Vuex constants in mutation-type.js, the Vuex modules in the subfolder modules (which are then loaded in the index.js).
- **API-Client** — API client is a service for calling up data. An http request is sent to the backend server or directly to the fediverse. It is also possible to configure a mock server.

### Process description

#### Block view level 1 - Get posts

![Class diagram](./diagrams/process-descriptions_fetch-posts–block-view-level-1.svg)

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

![Class diagram](./diagrams/process-descriptions_login-fetch–posts_block-view-level-2.svg)

- 1.0 The user logs in with his credential on the login page.

- 2.0 The router directs the user to his home page with the posts.

- 3.0 The components let the lifecycle created run.
- 3.1 In the created function, the `fetchCollectio()` is called from the _CollectionStore_.
- 3.2 `getPost()` is triggered as soon as the items in the _collectionStore_ are updated.

- 4.0 The _collectionStore_ calls the _apiServer_ to receive the collection data.
- 4.1 If the data comes back from the _apiServer_, the collection data is saved in the _collectionStore_
- 4.2 If a collection item is a create, it is checked whether the object is one of the post types and pulls the post out and adds it to the list of posts.
- 4.3 If a collection item is an update, it is checked whether the object is one of the post types and pulls the post out and adds it to the list of posts and deletes the old post from the list.
- 4.4 If a collection item is a delete, the ID is read out and filtered out of the post list.

- 5.0 Backend get request of the inbox of the user of the latest posts.
