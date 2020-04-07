# Follow
```json
{
  "@context": "https://www.w3.org/ns/activitystreams",
  "summary": "Sally followed John",
  "type": "Follow",
  "object": "https://mastodon.social/users/pascalmyself"
}
```

# Unfollow
The `$object` property is the object from the **Follow** example without `$object.@context`.

```json
{
    "@context": "https://www.w3.org/ns/activitystreams",
    "summary": "TiMESPLiNTER unfollowed",
    "type": "Undo",
    "to": "https://mastodon.social/users/pascalmyself",
    "object": {
    	"type": "Follow",
    	"object": "https://mastodon.social/users/pascalmyself" 
    }
}
```