# Brainstorming

## Open questions
* How to deal with a huge amount of follows from a single user. (User A follows 1000 other (remote) users)?
* Should we treat local users differently than remote users?
  * Out of scope
* In what format do we store content (especially text/notes)?
  * Maybe out of scope until we start implementing write access
* 

## User stories
- [ ] login user
- [ ] logout user
- [ ] delete user

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
POST /logout
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
DELETE /user/x
```

#### Response
```
204 No Content
```

```
403 Forbidden
```
