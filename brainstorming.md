# Brainstorming

## Open questions
* How to deal with a huge amount of follows from a single user. (User A follows 1000 other (remote) users)?
* Should we treat local users differently than remote users?
  * Out of scope
* In what format do we store content (especially text/notes)?
  * Maybe out of scope until we start implementing write access
* 

## User stories

### Phase 1
- [ ] login user
- [ ] logout user
- [ ] delete user
- [ ] show indbox of user
- [ ] show profile of user
- [ ] edit profile of user (summary, profile pic)
- [ ] follow another user
- [ ] unfollow a user
- [ ] list all following users
- [ ] search for users (webfinger)
- [ ] daemon for pulling following user's outboxes
- [ ] request pulling an outbox for a specific user
- [ ] request pulling all outboxed of following users
- [ ] auto update "all feed" in a specific interval

### Phase 2
- [ ] register a new user
- [ ] password forgotten
- [ ] like a post 
- [ ] comment a post 

### Phase n
- [ ] post an image
- [ ] post a note
- [ ] post a video
- [ ] share a post

## API doc
### Authorize user

#### Request
```
POST /token
Content-Type: application/json
{
  "username": "john.doe",
  "password": "secret"
}
```

#### Response
```
401 Access denied
```

```
204 No Content
Token: {jwt token}
```

### Logout user
#### Request
```
POST /user/{preferredUsername}/logout
Authorization: Bearer {jwt token}
```

#### Response
```
204 No Content
```

```
403 Forbidden
```

### Delete user

#### Request
```
DELETE /user/{preferredUsername}
```

#### Response
```
204 No Content
```

```
403 Forbidden
```

### Read inbox
See: https://www.w3.org/TR/activitypub/#inbox

```
GET /user/{preferredUsername}/inbox
```

### Post into outbox
See: https://www.w3.org/TR/activitypub/#outbox

```
POST /user/{preferredUsername}/outbox
```

* Follow: https://www.w3.org/TR/activitystreams-vocabulary/#dfn-follow
* Unfollow: https://www.w3.org/TR/activitystreams-vocabulary/#dfn-remove 

### Show following users
See: https://www.w3.org/TR/activitypub/#following

```
GET /user/{preferredUsername}/following
```
