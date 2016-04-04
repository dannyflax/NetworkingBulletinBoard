# NetworkingBulletinBoard

Project for CSE 3461. Full documentation here, because GitHub has better MD options. All JSON values are in String format, even if they represent numerical values. All timestamps are returned in seconds from the [Epoch](https://en.wikipedia.org/wiki/System_time).

## Introduction 

Each API call is encapsulated in the following JSON format:
#### Request
```
{
  "action_id" : action_id,
  "data" : {data}
}
```
*action_id* - Corresponds with a specific action, each of which listed as follows:
- 1 = [Join](#join)
- 2 = [Post](#post)
- 3 = [Leave](#leave)
- 4 = [Poll](#poll)
- 5 = [Expand](#expand)

These are discussed in more detail later.

*data* - The object passed to the action, as needed.

#### Response
```
{
  "successful" : successful,
  "data" : data
}
```
*successful* - 1 if action was executed successfuly, 0 if not.

*data* - The corresponding response to the action. Only valid if action was successful.

## Actions
A full description of all the actions that the server accepts.
### Join
Adds a user to the room if the name provided does not already exist in the room. Returns an error otherwise.

**Request:**
```
{
  "username" : username
}
```
*username* - The user to add to the room.

**Response:**
```
{
  "usernames": [list of usernames],
  "message_headers" : [list of message header objects],
  "user_id" : user_id
}
```
*usernames* - All the users who were in the room before the new user joined.

*message_headers* - The message header objects of the last two messages in the room. Message Header objects described at the bottom.

*user_id* - The numerical user_id assigned to the new user.

**Message header objects** are in the following format:
```
{
  "message_id" : message_id,
  "subject" : subject,
  "username" : username,
  "timestamp" : timestamp
}
```

### Post
Posts a new message in the room.

**Request:**
```
{
  "subject" : subject,
  "content" : content,
  "user_id" : user_id
}
```
*subject* - Message subject.

*content* - Content of the message.

*user_id* - The ID of the poster.

**Response:** No response object

### Leave
Leaves the room (presence no longer shown in other methods).

**Request:**
```
{
  "user_id" : user_id
}
```
*user_id* - The ID of the user to leave, as returned by the initial join.

**Response:** No response object

### Poll
Shows all new messages and users who have left after a given timestamp. This is meant to be called periodically so as to update the client's display.

**Request:**
```
{
  "timestamp" : timestamp
}
```
*timestamp* - Timestamp to limit responses by a specific date.

**Response:**
```
{
  "joins" : [list of user action objects],
  "leaves" : [list of user action objects],
  "message_headers" : [list of message header objects]
}
```

*joins* - Descriptions of actions involving users joining the room.

*leaves* - Descriptions of actions involving users leaving the room.

*message_headers* - List of header objects (as described [above](#join)) for messages that were posted.

**User action objects** are in the following format:
```
{
  "username" : username,
  "timestamp" : timestamp
}
```

### Expand
Shows the details of a specific message, given its message_id.

**Request:**
```
{
  "message_id" : message_id
}
```
*message_id* - ID of the message to expand

**Response:**
```
{
  "message_id" : message_id,
  "content" : content
}
```
*message_id* - ID of the message

*content* - Content of the message
