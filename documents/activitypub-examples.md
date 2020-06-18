# Follow
```
POST /user/{username}/outbox
Content-Type: application/activity+json

{
  "@context": "https://www.w3.org/ns/activitystreams",
  "type": "Follow",
  "id": "https://mitra-social.herokuapp.com/user/TiMESPLiNTER/follow/8548dbc5-abfc-411e-9a3b-e22149705212",
  "to": "https://mastodon.social/users/pascalmyself",
  "object": "https://mastodon.social/users/pascalmyself"
}
```

# Unfollow
The `$object` property is the object from the **Follow** example without `$object.@context`.
```
POST /user/{username}/outbox
Content-Type: application/activity+json

{
    "@context": "https://www.w3.org/ns/activitystreams",
    "summary": "TiMESPLiNTER unfollowed",
    "type": "Undo",
    "to": "https://mastodon.social/users/pascalmyself",
    "object": {
      "type": "Follow",
      "to": "https://mastodon.social/users/pascalmyself",
      "object": "https://mastodon.social/users/pascalmyself" 
    }
}
```
