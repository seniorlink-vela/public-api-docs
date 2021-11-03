# Table of Contents

- [Getting Started](#getting-started)
- [Utilizing public api](#utilizing-public-api)
- [Care teams](#care-teams)
- [User profiles](#user-profiles)
- [User suspensions](#user-suspensions)
- [Organizations](#organizations)
- [Care data](#care-data)
  - [Appointments](#appointments)
  - [Attachments](#attachments)
  - [Private Messages](#private-messages)
  - [Questionnaires](#questionnaires)
- [Rate Limiting](#rate-limiting)
- [Events](#events)
- [Queues](#queues)
- [Appendix of Event Types](event-types.md)

## Getting Started

### Pre-requisites

- Partner organization provisioned.
- Have a Vela account with Vela Admin access.

The following steps will have you sending your first Vela Public API request, so let's get started.

### Steps

1. Log into Vela Admin at <http://app.vela.care/admin/login>
2. Update your user's role with Public API permission by following these steps:
    1. Click on Organizations.
    2. Click on Update Roles from right menu under your Organization's details.
    3. Select the Role for your user (if unsure then navigate to your profile and see role under your name).
    4. Scroll down to Utilities section under the Administration tab.
    5. Click on execute for Public API.
    6. Click Save.
3. Navigate to Utilities and make note of the ```Client ID```.
4. To obtain your ```access_token``` from Vela's OAuth service use the cURL request below:

    ```sh
    curl -X "POST" 'https://app.vela.care/public/authentication/token' \
     -H 'Content-Type: application/x-www-form-urlencoded' \
     --data-urlencode "grant_type=password" \
     --data-urlencode "username=<insert-your-admin-username>" \
     --data-urlencode "password=<insert-your-admin-password>" \
     --data-urlencode "client_id=<insert-your-Client-ID>"
    ```

    Client_secret is optional. And so on success it returns ```200 OK``` and a JSON payload structured as:

    ```json
    {
        "access_token": "string",
        "client_id": "string",
        "client_name": "string",
        "email": "string",
        "expires_in": 0,
        "password_changed_at": "2020-08-06T18:47:09.438Z",
        "refresh_token": "string",
        "token_type": "string",
        "username": "string",
        "uuid": "string"
    }
    ```

    Excellent! Now you got your ```access_token``` and so hold onto that as it is a building block to your first request. Some notes to keep in mind, ```expires_in``` is in seconds. (ex. 14440s is 4 hours).

5. Let's build your first request. For this, you will send a [GET user-profiles](https://app.vela.care/public/api/docs/#!/admin/UserProfilesGet) request. And so the cURL looks like:

    ```sh
    curl "https://app.vela.care/public/api/v1/admin/user-profiles" \
        -H 'Authorization: Bearer <insert-your-access-token>'
    ```

     And so on success it returns ```200 OK``` and a JSON payload structured as:

     ```json
        {
            "meta": {
                "page": 1,
                "page_size": -1,
                "record_count": 60,
                "total_pages": 1
            },
            "user_profiles": [
                {
                    "address1": null,
                    "address2": null,
                    "city": null,
                    "country": null,
                    // ....
                }
            ]
        }
     ```

6. Visit Vela Public API's [Swagger docs](https://app.vela.care/public/api/docs/) to see all currently available endpoints.

## Utilizing public api

All endpoints require authorization -- to use the public api the caller must have the public api permission associated with their account.

![image](images/admin-roles.png)

The APIs are broken up into several sections - admin for user, organization, and care team data, care data for information regarding the care of a specific user, as well as data about communication between users, and the events section -- which uses queues and webhooks to inform the partner of what data has been created or changed as it happens within the system.

This is a Restful api, and follows standard conventions.  A user must have the public_api permission in Vela to access it.

With the exception of the authentication endpoint, all endpoints require a valid authorization bearer token in the header and take in request data that is content-type "application/json". Operations can be performed against all of them.

Operations against an existing user profile require the id parameter.  This ID is the reference ID provided to Vela when the record is created, not the internal id to Vela. If a reference ID was not supplied, Vela generated one that is unique to your partner organization and is supplied for ease of integration. This ID is also viewable in the admin UI as the "External Reference ID".

Example of flow:

1. Get a token
2. Get the user by id or email address
3. Patch the user by id

## Admin

This is all information related to the admin user experience.

### Care teams

A care team is a care recipient and the professional and non-professional users dedicated to their care.
A care team has its own id used to reference it.
The care team's ID can be recovered via the /api/v1/admin/care-teams/consumer/{consumer_user_id} endpoint, (where consumer_user_id is the reference ID); the "id" returned is the ID of the care team that the care recipient/consumer belongs to.

Operations:

- Fetch all care teams.
- Authorize a care team.
- Add or update a care team member.
- Remove (delete) a member of a care team.
- Get a care team for the provided consumer user id.

Typical operation for creating a care team: Create a care recipient. GET the care team via the care recipient's "ID" (external reference ID). Add other users to the care team via POSTing new members to it. Authorize the care team, unless it's intended that the care recipient will log in and do so.

No non-admin user can operate on a care team until the care team has been authorized via the API or by the care recipient when they log in for the first time. You never need to create a care team. Creating a care recipient creates a care team around them.

### User profiles

A user is a person who exists in the Vela applications.
All user manipulations are under user-profiles in the API.
There are 4 categories of users in Vela:

- Care recipients (Patients, Members, etc)
- Caregivers
- Professionals
- Administrators.

Every user is a member of an organization, and visibility of other users is controlled by the organization hierarchy.

Operations:

- GET a list of users.
- Create users.
- GET an individual user via external reference ID.
- GET an individual user via GET /api/v1/admin/user-profiles/by-reference/email/{user_email} - accepts either an email address or username via the 'user_email' parameter.
- Update user via PUT or PATCH.

To update a user's ID via PUT or PATCH you can provide their current ID (External reference ID) in the "id" field and supply the new id (external reference ID) in the body of the call.

### User suspensions

Putting a user on suspension is like a temporary disenrollment from the program. Descriptively, suspensions are called "pauses" in the admin UI.
Any questionnaire assignments with a start date that falls between the start date and end date of a suspension will be invisible to caregivers and care recipients, and will show up to professional users as 'suspended'. The typical use case for this is when questionnaires are assigned on some schedule (daily, weekly, etc.) and there is an operational reason why those periodic questionnaires shouldn't be seen during that time. As an example, if a caregiver is caring for a care recipient, and the care recipient is hospitalized; during that hospitalization period, the questionnaire assignments asking the caregiver for how the care recipient is doing on that day or what services the caregiver may have rendered wouldn't be appropriate. They will not be responsible for completing questionnaires during a suspension period.

A suspension requires a start date, but the end date is optional; if not provided the suspension will start at the start time and continue on indefinitely; this is helpful when, for example, the duration of the care recipient's hospital stay is not yet known, and can be added once it is.
  All operations to modify one require the id of the suspension.
  Operations:

  - GET list by user id.
  - POST to user id.
  - Update (PUT), DELETE, GET (by id).

### Organizations

All organizations descend from a partner_id -- the root of your organization tree.
Orgs can be added anywhere in your tree or moved. Moving a parent organization moves all its children with it.
Example of creating a sub org within an organization via the admin UI:

  ![image](images/create-sub-org.png)

  ![image](images/create-sub-org-result.png)

Operations:

- Create (POST to the id of the parent organization).
- Update by id (PUT and PATCH).
- List all organizations that are descendants of the id (GET).
- GET an individual org by ID.

## Care data

This is all data specific to a care team - its messaging, and questionnaires related to patient care.

### Appointments

Operations:

- Create (POST an appointment from a provider and can also optionally share with other members in a care team).
- Update an appointment by ID (PUT).
- Delete an appointment by ID.

### Attachments

Operations:

- Create (POST an attachment and share with care teams).
- Get an attachment by ID.
- GET (Download the content of an attachment).

### Private Messages

The post to private messages allows allows the user to send a message to a group of users on a care team.  The focus_id identifies the patient the message is about.  If the team_chat is set to true it uses a team channel on the foc_id's care team.
Otherwise it finds or builds a chat to the members of the to_list - in a chat for the focus_id.  An existing chat channel will be used if one exists - otherwise a new one will be built.
The get endpoint gets any message that fits the parameters supplied - for a given user (required), and for a date interval, the chat logs are searched for any message that matches the criteria.

Operations:

- Create(POST a private message to a user from a provider on the care team).
- Create(POST a private message to a default chat of a care team by specifying a default chat key)
- GET private messages sent to a user and/or in a message thread.

### Questionnaires

The submission by id endpoint gets one submitted questionnaire that matches the id.  The GET endpoint returns any questionnaire for the required user that fits the criteria.

Operations:

- Create(POST Questionnaire assignment).
- GET questionnaire assignment list.
- Get a questionnaire submission by id.
- Get a list of questionnaires for this user.

## Rate Limiting

Access to the vela APIs is rate limited by a simple leaky bucket algorithm with a shared key so multiple server instances share the same counter.
If you have exceeded your allotment, a 429 error can be returned from any endpoint.
Usage statistics can be viewed at the "/events/usage-by-type" endpoint.

## Events

The queues allow data to be pulled from the system to the partner.  The events are a time series of everything happening in vela.
The different types of events are as follows:
  user-login
  user-created
  user-updated
  organization-created
  organization-update
  organization-deleted
  user-suspension-created
  user-suspension-updated
  user-suspension-deleted
  care-team-created
  care-team-updated
  private-message-sent
  private-message-updated
  alert-message-created
  alert-message-updated
  alert-message-deleted
  questionnaire-created
  questionnaire-updated
  questionnaire-deleted
  questionnaire-assignment-created
  questionnaire-assignment-updated
  questionnaire-assignment-deleted
  questionnaire-assignment-submitted
    A current list of event_types can be gotten from the event-types GET endpoint.

## Queues

A queue is defined for you at each partner organization.  It can be edited with the patch endpoint -- and the events types desired.
The default is to receive them all.
Information can be received about the queue by calling the get endpoint.
It can be updated with the patch endpoint.
Set the event_types value to the ones you wish to receive - and empty array is every event by default.
Whenever desired you can pull events from the queue using GET /api/v1/events/queue/events.
Every queue has a watermark, when you GET from the queue it returns the next X records (for now a max of 100).
The get returns {

```json
{
    "events": [
        {
            "created_at": "2020-08-07T16:37:20.182Z",
            "event_type": "string",
            "event_type_id": 0,
            "id": 0,
            "message_source": "string",
            "message_timestamp": "2020-08-07T16:37:20.182Z",
            "message_uuid": "string",
            "organization_id": 0,
            "partner_id": 0,
            "payload": {}
        }
    ],
    "last_read_index": 0
}
```

You receive an array of records and the last_read_index -- which is your new watermark.
After you have received the records you should update the watermark -- to the value returned from the GET. PUT /api/v1/events/queue/watermark
This advances the cursor in the queue.  This is done to ensure that the delivery has occurred and no records are lost, since the system only knows that the records were sent - not that they were successfully received.
The watermark and event_types are completely under your control.  You can reset them at will.  You can rewind at will and change what event types at any time.

Operations:

- Return a queue for the organization of an admin or for the provided organization if the caller is a service user.
- Return events of the queue for the organization of an admin or for the provided organization if the caller is a service user.
- Update the watermark of a queue for the organization of an admin or for the provided organization if the caller is a service user.
