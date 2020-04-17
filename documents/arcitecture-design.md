# Architecture & Design

## Backend

### Block view level 1

![Class diagram](./diagrams/architecture-block-view-level-1.svg)

* **API:** The API reflects the service with its endpoints as described in the ActivityPub standard (for example: inbox/outbox/user endpoints) plus some additional endpoints not discussed in ActivityPub standard document but necessary for the proper functioning of the application (for example: register/token issue endpoint). In general the API component MUST be implemented non-blocking in regard of calls to remote servers. Thus all calls to remote servers MUST be reflected by tasks pushed into the _**Queue**_ and handled asynchronously. This guarantees fast response times for the API. Although there MAY be some exceptions like pulling a remote user's outbox explicitly by a call to a dedicated endpoint for this.
* **Worker:** The worker processes the tasks in the _**Queue**_ and executes all the calls to external servers to push or pull information requested in the currently processed task. The worker MAY push follow up tasks into the _**Queue**_.
* **Queue:** The queue holds all the open tasks that need to be processed by the _**Worker**_ component.
* **DB:** The database component in general stores all the information generated on the server through either the _**API**_ or _**Worker**_ as well as external fetched content through the _**Worker**_ component.
* **File system:** All media data like images, videos, etc. either produced through API calls or through calls to remote servers by the _**Worker**_ is stored in the file system and references to the location are stored in the _**DB**_.

### Class diagram
![Class diagram](./diagrams/class-diagram.svg)

## Frontend

### Block view level 1

![Class diagram](./diagrams/architecture-frontend-block-view-level-1.svg)
