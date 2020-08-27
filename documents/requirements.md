# System definition

## System context

![system context](./diagrams/system-context.svg)

## Actors

### User

The user is a natural person who wants to know what's going on in the world.

### Server

The server is the remote ActivityPub server. This can be your own server or a different one.

# Functional requirements

## Use Case

### Template

| Section             | Content |
| ------------------- | ------- |
| Identifier          | -       |
| Name                | -       |
| Author              | -       |
| Priority            | -       |
| Criticality         | -       |
| Origin              | -       |
| Responsibility      | -       |
| Description         | -       |
| Triggering Event    | -       |
| Actor               | -       |
| Precondition        | -       |
| Postcondition       | -       |
| Exception scenarios | -       |
| Quality             | -       |

### User Case

![use case user](./use-cases/use-case-user.svg)
Section | Content
------------------------| -------------
Identifier | UC-01
Name | Registration
Author | Pascal, Franco
Priority | High importance for system success. Technological risk low
Criticality | High
Responsibility | Pascal, Franco
Description | The user registers on the Mitra site with his email, preferred username and password.
Triggering iEvent | Click on the registration button.
Actor | User
Precondition | Email or preferred username is not registered.
Exception scenarios | Email or preferred username already exists. The repeating password does not match.

| Section             | Content                                                                          |
| ------------------- | -------------------------------------------------------------------------------- |
| Identifier          | UC-02                                                                            |
| Name                | Login                                                                            |
| Author              | Pascal, Franco                                                                   |
| Priority            | High importance for system success. Technological risk low                       |
| Criticality         | High                                                                             |
| Responsibility      | Pascal, Franco                                                                   |
| Description         | The user sign in with his preferred username and password on the login of mitra. |
| Triggering Event    | User calls up the mitra page and lands on the login page.                        |
| Actor               | User                                                                             |
| Precondition        | User has registered and knows his credential.                                    |
| Exception scenarios | Credential is not correct.                                                       |

| Section          | Content                                                      |
| ---------------- | ------------------------------------------------------------ |
| Identifier       | UC-03                                                        |
| Name             | Logout                                                       |
| Author           | Pascal, Franco                                               |
| Priority         | Middle importance for system success. Technological risk low |
| Criticality      | Middle                                                       |
| Responsibility   | Pascal, Franco                                               |
| Description      | The user logged out of the Mitra page.                       |
| Triggering Event | Click on the logout button.                                  |
| Actor            | User                                                         |
| Precondition     | The user is logged in.                                       |

| Section             | Content                                                         |
| ------------------- | --------------------------------------------------------------- |
| Identifier          | UC-04                                                           |
| Name                | Edit User                                                       |
| Author              | Pascal, Franco                                                  |
| Priority            | Middle importance for system success. Technological risk middle |
| Criticality         | Middle                                                          |
| Responsibility      | Pascal, Franco                                                  |
| Description         | The user can edit his personal data or his password.            |
| Triggering Event    | User calls up the mitra page and lands on the login page.       |
| Actor               | User                                                            |
| Postcondition       | Token is correct.                                               |
| Exception scenarios | The repeating password does not match.                          |

| Section             | Content                                                      |
| ------------------- | ------------------------------------------------------------ |
| Identifier          | UC-05                                                        |
| Name                | Delete User                                                  |
| Author              | Pascal, Franco                                               |
| Priority            | Low importance for system success. Technological risk middle |
| Criticality         | Low                                                          |
| Responsibility      | Pascal, Franco                                               |
| Description         | The user can delete his account.                             |
| Triggering Event    | Click the Delete button.                                     |
| Actor               | User                                                         |
| Precondition        | The user must confirms that the account will be deleted.     |
| Postcondition       | Token is correct.                                            |
| Exception scenarios | The repeating password does not match.                       |

| Section             | Content                                                                                    |
| ------------------- | ------------------------------------------------------------------------------------------ |
| Identifier          | UC-06                                                                                      |
| Name                | Forgot Password                                                                            |
| Author              | Pascal, Franco                                                                             |
| Priority            | Low importance for system success. Technological risk high                                 |
| Criticality         | Low                                                                                        |
| Responsibility      | Pascal, Franco                                                                             |
| Description         | If the user no longer knows his password, he can reset the password by entering his email. |
| Triggering Event    | Click the Forgot Password Link.                                                            |
| Actor               | User                                                                                       |
| Postcondition       | E-Mail exists.                                                                             |
| Exception scenarios | The email does not exist.                                                                  |

| Section          | Content                                                                                                                            |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| Identifier       | UC-07                                                                                                                              |
| Name             | Search User                                                                                                                        |
| Author           | Pascal, Franco                                                                                                                     |
| Priority         | Middle importance for system success. Technological risk high                                                                      |
| Criticality      | Middle                                                                                                                             |
| Responsibility   | Pascal, Franco                                                                                                                     |
| Description      | The user enters the desired webfinger id in the search field. as a result he gets a user with his information where he can follow. |
| Triggering Event | Click the search button.                                                                                                           |
| Actor            | User                                                                                                                               |
| Precondition     | The user is login.                                                                                                                 |
| Postcondition    | Token is correct.                                                                                                                  |

### Posts Case

![Usetr](./use-cases/use-case-posts.svg)
Section | Content
------------------------| -------------
Identifier | UC-08
Name | Show Posts
Author | Pascal, Franco
Priority | High importance for system success. Technological risk high
Criticality | High
Responsibility | Pascal, Franco
Description | The post is displayed to the user from the user he is following.
Triggering Event | The login redirects to the home with the posts, the home link is clicked or system pulling with a intervall.
Actor | User
Precondition | The user is login.
Postcondition | Token is correct.

| Section          | Content                                                                       |
| ---------------- | ----------------------------------------------------------------------------- |
| Identifier       | UC-09                                                                         |
| Name             | Toggle show in reply to post                                                  |
| Author           | Pascal, Franco                                                                |
| Priority         | Low importance for system success. Technological risk middle                  |
| Criticality      | Low                                                                           |
| Responsibility   | Pascal, Franco                                                                |
| Description      | The post to which the displayed post was replied to should also be displayed. |
| Triggering Event | The post should be made visible and invisible again with one click.           |
| Actor            | User                                                                          |
| Precondition     | The user is login.                                                            |
| Postcondition    | Token is correct.                                                             |

| Section          | Content                                                                                  |
| ---------------- | ---------------------------------------------------------------------------------------- |
| Identifier       | UC-10                                                                                    |
| Name             | Receive activity                                                                         |
| Author           | Pascal, Franco                                                                           |
| Priority         | High importance for system success. Technological risk high                              |
| Criticality      | High                                                                                     |
| Responsibility   | Pascal, Franco                                                                           |
| Description      | The server receives activities from users other servers on which the mitra user follows. |
| Triggering Event | Get data is triggered with a defined interval.                                           |
| Actor            | Server                                                                                   |

### Follow Case

![Usetr](./use-cases/use-case-follow.svg)

| Section          | Content                                                         |
| ---------------- | --------------------------------------------------------------- |
| Identifier       | UC-11                                                           |
| Name             | Follow actor                                                    |
| Author           | Pascal, Franco                                                  |
| Priority         | Height importance for system success. Technological risk middle |
| Criticality      | Height                                                          |
| Responsibility   | Pascal, Franco                                                  |
| Description      | The user can follow another user.                               |
| Triggering Event | Click the follow button of the desired user.                    |
| Actor            | User                                                            |
| Postcondition    | Token is correct.                                               |

| Section          | Content                                                         |
| ---------------- | --------------------------------------------------------------- |
| Identifier       | UC-12                                                           |
| Name             | Unfollow actor                                                  |
| Author           | Pascal, Franco                                                  |
| Priority         | Middle importance for system success. Technological risk middle |
| Criticality      | Middle                                                          |
| Responsibility   | Pascal, Franco                                                  |
| Description      | The user no longer wants to follow another user.                |
| Triggering Event | Click the unfollow button of the desired user.                  |
| Actor            | User                                                            |
| Postcondition    | Token is correct.                                               |

## Conditions

### Naming Condition

![namingCondition](./diagrams/naming-condition.svg)

## Data structures of the system interfaces

- [ActivityStreams Object](https://www.w3.org/ns/activitystreams#class-definitions)

# Non-functional requirements

## Quality requirements

### Availability

- The system must be accessible at all times.

### Reliability

- The correct account is loaded when you log in
- The system should display all posts that the user is following
- The system should display the correct post when filtering for users
- The system should add the right user to the following list

### Performance

- The response times should be less than 1 second if possible

### Security

- The system is protected by a password

### Usability

- The user should be able to use the application without training

### Changeability

- Requirements must be evolutionary
- Benchmarked against the baseline requirements

## Boundary conditions

### Procedure

- Kanban(Agile)

### Standards

- [ActivityPub](https://www.w3.org/TR/activitypub/)
- [ActivityStreams](https://www.w3.org/ns/activitystreams)
