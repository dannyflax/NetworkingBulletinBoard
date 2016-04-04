# NetworkingBulletinBoard

Project for CSE 3461. Full documentation here, because GitHub has better MD options. All JSON values are in String format, even if they represent numerical values.

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
- 1 = Join
- 2 = Post
- 3 = Leave
- 4 = Poll
- 5 = Expand

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
#### Join
Adds a user to the room if the name provided does not already exist in the room. Returns an error otherwise.

Request:
```
{
  "username" : username
}
```
*username* - The user to add to the room.

Response:
```
{
  "usernames": [list of usernames],
  "message_headers" : [list of message headers],
  "user_id" : user_id
}
```
*usernames* - All the users who were in the room before the new user joined.

*message_headers* - The message header objects of the last two messages in the room. Message Header objects described at the bottom.

*user_id* - The numerical user_id assigned to the new user.

#### Post
Posts a new message in the room.

Request:
```

```

Response:
```

```

#### Leave
Leaves the room (presence no longer shown in other methods).

Request:
```

```

Response:
```

```

#### Poll
Shows all new messages and users who have left after a given timestamp

Request:
```

```

Response:
```

```

#### Expand
Shows the details of a specific message, given its message_id.

Request:
```

```

Response:
```

```
