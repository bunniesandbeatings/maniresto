# ManiRESTo
Using [RESTful](http://en.wikipedia.org/wiki/Representational_state_transfer) resources in an easy to reason about manner.

Including the good bit's of [HATEOAS](http://en.wikipedia.org/wiki/HATEOAS), heuristically applied to every-day API development.

## Resources

* Are consistant
  * Same representation each request
  * Same representation for each verb
* Do not need to map to your underlying data model directly
  * Light representations to clarify meaning or intent

## Verbs
  * Common verbs are GET, PUT, DELETE, POST
  * Don't create new verbs
  * Don't RPC
    * Favor `GET path/to/resources` over `GET resource/index`
    * Favor `DELETE path/to/resource` over `GET path/to/resource/delete`
    * Favor `GET path/to/invoice/taxes` over `get path/to/invoice/calculate_taxes`
 
## Status Codes
  * Are often sufficient to convey meaning
  * Use over requiring loading another resource for details
    * Do not require user to use something else to find out that permission
    * [Might be a little mean](#enumerating-permissions)

## URIs


# Notes

## Enumerating Permissions
If a resource returns a 403 or 404 due to permissions, eg:

```
GET path/to/things/resource1 -> 403: Forbidden
GET path/to/things/resource2 -> 403: Forbidden
GET path/to/things/resource3 -> 400	
```

Consider providing collection level permissions (as well as maintaining Status Codes):

```
GET path/to/things -> 
  { 
    'resource1': { 'status': 403, 'uri': 'path/to/things/resource1' },
    'resource2': { 'status': 403, 'uri': 'path/to/things/resource2' },
    'resource3': { 
      'uri': 'path/to/things/resource3',
      'status': 400,
      'summary_field': 'I am a summary collection field'
    }
  }
```  
  
# TODO
* Link rel. Obviously.