# NetworkingBulletinBoard
Project for CSE 3461. Full documentation here, because GitHub has better MD options.

Each API call is encapsulated in the following format:
### Request
```
{
  "action_id" : action_id,
  "data" : data
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

### Response
```
{
  "successful" : successful,
  "data" : data
}
```
*successful* - 1 if action was executed successfuly, 0 if not.

*data* - The corresponding response to the action. Only valid if action was successful.
