POCs
====

Notes about POCs to clarify and verify capabilities and if the plans are sane and feasible.


A minimal tool with multiple users and Firebase
-----------------------------------------------

Goals:

- [x] Users can login with Google and another example social provider (Twitter)
  - Let user select provider, create appropriate provider for example `var provider = new firebase.auth.GoogleAuthProvider();` or `var provider = new firebase.auth.TwitterAuthProvider();` and initiate the login with the selected provider `firebase.auth().signInWithPopup(provider)`

- [x] Users have their isolated storage areas
  - Possible by structuring the data with the username included in the tree,
    and appropriate [rules][rules] that restrict user writes and reads to that sub-tree.
    See examples below.
  - Make sure to use validation rules with length limits on all fields
  - Make sure to define indexes before deployment

- [x] Admin can impose restrictions depending on the user, to make paid features possible
  - Rules can reference any node in the storage -> limites can be imposed in sub-trees not accessible by users
  - All data is visible on firebase console, and admin can delete abusive users
  - Possible to prevent users from creating junk fields with `"$other": { ".validate": false }`

- [x] Paid features are possible
  - Easy on Android, where the source code is protected
  - Do not publish the URL to the web app, or take it down

Example of organizing content in a way that users have their individual isolated areas:

    {
      "rules": {
        "users": {
          "$uid": {
            ".write": "$uid === auth.uid"
            ".read": "$uid === auth.uid"
          }
        }
      }
    }

Other interesting examples and useful links:

- https://firebase.google.com/docs/database/security/securing-data

- https://codelabs.developers.google.com/codelabs/firebase-web

Other useful commands:

    # replace database content
    firebase database:set / ./initial_messages.json

    # deploy database rules
    firebase deploy --only database

    # deploy everything except functions (what are functions???)
    firebase deploy --except functions

    # deploy to cloud hosting
    firebase open hosting:site

Other notes:

- The data storage is not distributed under user accounts, but all are stored under your app

- Multiple providers can be linked, though this is not important to me at all right now.
  https://firebase.google.com/docs/auth/web/account-linking

### Implementation

Transform the FriendlyChat to a primitive HabitMaker client,
featuring the critical target goals.

- [ ] Design the storage schema for Habits and HabitLogs for multiple users
  - [ ] Schema for Habits, with rules
  - [ ] Schema for HabitLogs, with rules

- [ ] Make the minimal changes to FriendlyChat to create Habits and HabitLogs
  - [ ] Enter habits with message format: habit:name:type:days
  - [ ] Enter habit logs with message format: log:name
  - [ ] Verify correct entry per user in Firebase console

- [ ] Make the minimal changes to FriendlyChat to view Habits and HabitLogs
  - [ ] View Habits
  - [ ] View HabitLogs

- [ ] Verify with multiple users (Google and Twitter)

- [ ] Make it impossible to add more than 3 Habits by one of the users but not the other
  - [ ] Design the rule
  - [ ] Verify the Google user cannot add more than 3, and the Twitter user can

- [ ] Save the POC in a separate repo

[rules]: https://firebase.google.com/docs/database/security/
