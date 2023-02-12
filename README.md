
# Blog-Micro

## Monolith Architecture
![Screenshot (230)ewq](https://user-images.githubusercontent.com/97042529/218295513-fa161d6b-4022-43e4-ab4c-a482025c2141.png)

A monolith contains all the routing, all the middleware, all the business logic and all the database access required to implement all features of our application.

## Microservices
![Screenshot (229)jg](https://user-images.githubusercontent.com/97042529/218295470-f96a4eac-2c50-4cd6-bdbb-772d24bd4f28.png)

A single microservice contains all the routing, all the middleware, all the business logic and all the database access required to implement one features of our application.

# About this app:

A simple microservice blog application where users can post the comments regarding any blog. Users can also delete the comments from a particular blog.

This comments are fetched to the frontend with the help of axios and then displayed on the main page. Comments are saved to the local storage of MongoDB.

This application conatains various services: 

a) Posts Service: Responsible for i) Creation of Posts
                                 ii) Listing of all Posts

b) Comments Service: Responsible for i) Creating a Comment 
                                     ii) Listing of all comments

c) Event Bus: Responsible for receiving the events and publishing to the listeners. Build using express.js

d) Query Service: The goal of this service is to have one service
that we can make request to get a full listing of all the different post and its associated comments.

e) Moderation Service: A filtering feature which keeps an eye on a particular comment. Suppose if the comment is misleading or not appropriate then we have the filtering feature. "Approved", "Rejected" ,"Pending" are the three scenerios which comes under this service. 





## API Reference

### Post Service

###### Get all Post

```http
  GET http://posts.com/posts
```
###### Create Post

```http
  POST http://posts.com/posts/create
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `Number` | **Required**. Id of item to fetch |
| `title`      | `String` | **Required**. title of item to fetch |

### Comment Service

###### Get all Comments

```http
  GET http://posts.com/posts/:id/comments
```
###### Create Comment

```http
  POST http://posts.com/posts/${postId}/comments
```
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `Number` | **Required**. Id of item to fetch |
| `content`      | `String` | **Required**. content of item to fetch |
| `postId`      | `Number` | **Required**. postId of item to fetch |

### Event Bus

###### Get all Events

```http
  POST http://posts.com/posts/events
```
###### Particular Event

```http
  POST http://posts-clusterip-srv:4000/events
  POST http://comments-srv:4001/events
  POST http://query-srv:4002/events
  POST http://moderation-srv:4003/events
```

### Query Service

###### Get all Query

```http
  GET http://event-bus-srv:4005/events
```
###### Query Info 

```http
  POST http://posts.com/posts/${postId}/comments
```
Contains two parameters:

i) Data
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `Number` | **Required**. Id of item to fetch |
| `title`      | `String` | **Required**. content of item to fetch |

ii) Type

a)"Post Created"
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `Number` | **Required**. Id of item to fetch |
| `title`      | `String` | **Required**. content of item to fetch |

b)"Comment Created"
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `Number` | **Required**. Id of item to fetch |
| `content`      | `String` | **Required**. content of item to fetch |
| `postId`      | `number` | **Required**. postId of item to fetch |
| `status`      | `String` | Fetched to Frontend |

c)"Comment Updated"
| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `Number` | **Required**. Id of item to fetch |
| `content`      | `String` | **Required**. content of item to fetch |
| `postId`      | `number` | **Required**. postId of item to fetch |
| `status`      | `String` | Fetched to Frontend |

## Tech Stack

**Client:** React , Bootstrap

**Server:** Nodejs , Docker , Kubernetes


## Screenshots

![Screenshot (231)saf erwr](https://user-images.githubusercontent.com/97042529/218298219-c73ce65d-25e8-4c37-a89c-a49378056aff.png)

