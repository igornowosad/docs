# REST API

Main question when designing API is, whether or not specify someting as parameter, query value or send it in request body 
or header. I've prepared here simple description of the most reasonable API interface. I hope it'll make this process easier 
for you to understand and implement.

### What to put in parameters?

In parameters you put only identifier of entity you want to modify/get/delete. Identifier in most cases is object ID, but it
can be name as well.

Some axample:

`GET /customers/:id` - get single customer data by customer ID

In case of GET and DELETE requests, you __should not__ send additional data in body, becouse in DELETE they're simply 
ignored when sending request and in GET it is not good practise and server doesn't have to take them into account
when fulfilling a request.

### What convention of sending data to use when sending different requests?

In case of sending __filter__, __sort__ etc properties, you should always send them __in query__. They're data, that are not 
affecting response data itself, just limiting response data amount and order.

#### GET

GET is used to __get__ some data and shouldn't be used to in any way modify or create anything. If this is required in 
application flow, consider using POST or PUT/PATCH and return needed data. 

```javascript
GET /customers?sort=-name&filter=name&query=Johnsson
// response: 200, array of customer objects which fulfill given filter and are sorted in ascending order ('-' = asc, '+' = desc)
```
```javascript
GET /customers/:id?fields=name,nip
// response: 200, customer object with specified fields and id and metadata (e.g. createdBy, modifiedBy, createdAt...)
```

#### PUT, PATCH

PUT/PATCH is used to modify specified entities. 
Send only __identifiers__ of modified entity __in params__, the rest should be sent in body.

```javascript
PUT /customers/:id
body: { name: ..., nip:... } 
// response: 200, full modified object with applied changes, the structure should be the same as when getting single object
// on: GET /customers/:id
```

#### POST

POST is used to __create__ new entity object. There __should not__ be sent any __identifier__ in this request, becouse POST 
is meant to create new entity independent on anything else. Any __relations to another entities__ etc should be sent __in 
body__.

```javascript
POST /customers
body: { name: ..., nip: ... }
// response: 200, full object of created customer with metadata. Usually corresponds to what is returned when getting single 
// customer on GET /customers/:id
```

### Other types of specifying endpoints parameters per use case:

1. when getting projects of given user: 
`GET /users/:id/projects`
1. when getting users associated with given project:
`GET /projects/:id/users`

### More resources
http://blog.octo.com/en/design-a-rest-api/
