# Appendix of Event Types

| id | slug                               |
| ---|------------------------------------|
| 1  | user-login                         |
| 2  | user-created                       |
| 3  | user-updated                       |
| 4  | organization-created               |
| 5  | organization-updated               |
| 6  | organization-deleted               |
| 7  | user-suspension-created            |
| 8  | user-suspension-updated            |
| 9  | user-suspension-deleted            |
| 10 | care-team-created                  |
| 11 | care-team-updated                  |
| 12 | private-message-sent               |
| 13 | private-message-updated            |
| 14 | alert-message-created              |
| 15 | alert-message-updated              |
| 16 | alert-message-deleted              |
| 17 | questionnaire-created              |
| 18 | questionnaire-updated              |
| 19 | questionnaire-deleted              |
| 20 | questionnaire-assignment-created   |
| 21 | questionnaire-assignment-updated   |
| 22 | questionnaire-assignment-deleted   |
| 23 | questionnaire-assignment-submitted |
| 24 | notification-sent                  |
| 25 | notification-received              |
| 26 | notification-failed                |
| 27 | notification-opened                |
| 28 | notification-bounced               |
| 29 | notification-clicked               |
| 30 | private-message-read               |
| 31 | user-activity                      |
| 32 | care_path_topic_assignment_created |
| 33 | care_path_topic_assignment_updated |
| 34 | care_path_topic_assignment_deleted |
| 35 | user-application-access            |

## Structure of Each Event-Type

- [Event-type 1](#event-type-1)
- [Event-types 2, 3](#event-types-2-3)
- [Event-types 4, 5, 6](#event-types-4-5-6)
- [Event-types 7, 8, 9](#event-types-7-8-9)
- [Event-types 10, 11](#event-types-10-11)
- [Event-type 12](#event-type-12)
- [Event-type 13](#event-type-13)
- [Event-type 14, 15, 16](#event-type-14-15-16)
- [Event-types 17, 18, 19](#event-types-17-18-19)
- [Event-types 20, 21, 22, 23](#event-types-20-21-22-23)
- [Event-types 24, 25, 26, 27, 28, 29](#event-types-24-25-26-27-28-29)
- [Event-type 30](#event-type-30)
- [Event-type 31](#event-type-31)
- [Event-types 32,33,34](#event-types-32-33-34)

### Event-type 1

  ```json
  {
      "client_application": "ADMIN_WEB",
      "oauth_client_id": "14g1009f-f761-4d44-9ee3-5caacada6dc6.vela.care",
      "recorded_at": "2019-04-24T15:15:39Z",
      "user_id": "vela_example_347",
      "username": "example_cm"
  }
  ```

### Event-types 2-3

  ```json
  {
      "address_line1": null,
      "address_line2": null,
      "address_line3": null,
      "address_line4": null,
      "address_line5": null,
      "address_line6": null,
      "archived_at": null,
      "archived_by": null,
      "birthday": null,
      "city": null,
      "country": null,
      "created_at": "2019-04-24T17:51:03Z",
      "created_by": "V00000000010000000001",
      "disabled_at": null,
      "disenrolled_at": "3016-03-25T00:00:00Z",
      "email": "zzzzz+whynoput@gmail.com",
      "enrolled_at": "2019-04-24T17:50:01Z",
      "extended_properties": null,
      "first_name": "mike",
      "first_sign_in_at": null,
      "gender": "UNSPECIFIED",
      "id": "V00230091790000000001",
      "language": "en",
      "last_name": "example-ppe",
      "middle_name": null,
      "needs_onboarding": false,
      "organization_id": 1,
      "partner_id": 1,
      "primary_phone_number": "1115551212",
      "second_email": null,
      "secondary_phone_number": null,
      "state": null,
      "tertiary_phone_number": null,
      "timezone": "America/New_York",
      "updated_at": "2019-04-24T17:51:03Z",
      "updated_by": "V00000000010000000001",
      "user_type_category": "ADMIN",
      "user_type_id": 105,
      "user_type_name": "Admin",
      "username": "zzzzz+whynoput@gmail.com",
      "uuid": "eddc81ed-f5f5-4afe-91cd-2e595da922b8",
      "zip": null
  }
  ```

### Event-types 4-5-6

  ```json
  {
      "address_line1": null,
      "address_line2": null,
      "city": null,
      "created_at": "2019-04-24T22:10:18Z",
      "created_by": "vela_example-dd370b11",
      "email": null,
      "id": 392,
      "name": "Chewie",
      "parent_id": 83,
      "partner_id": 4,
      "phone_number": null,
      "state": null,
      "updated_at": "2019-04-24T22:10:18Z",
      "updated_by": "vela_example_da2161f4-246e-446f-ae38-1315dd370b11",
      "zip": null
  }
  ```

### Event-types 7-8-9

  ```json
  {
      "created_at": "2019-04-25T12:45:51Z",
      "created_by": "vela_defaul-example",
      "description": "23 to 26 Edited",
      "end_at": "2019-04-27T03:59:59Z",
      "id": 857,
      "start_at": "2019-04-23T04:00:00Z",
      "updated_at": "2019-04-25T12:46:11Z",
      "updated_by": "vela_example-9",
      "user_id": "vela_example-s01a"
  }
  ```

### Event-types 10-11

  ```json
  {
      "authorized_at": null,
      "authorized_by": null,
      "consumer_user_id": "V00002311830000945004",
      "created_at": "2019-04-24T22:11:32Z",
      "created_by": "vela_example-sfdg",
      "id": 3850,
      "member_changes": null,
      "members": [],
      "organization_id": 4,
      "status": "created",
      "updated_at": "2019-04-24T22:11:32Z"
  }
  ```

### Event-type 12

  ```json
  {
      "additional_data": null,
      "attachment_id": null,
      "chat_message_id": 21556,
      "content": "hello",
      "created_at": "2019-04-24T15:42:52Z",
      "message_thread": {
          "confidential": true,
          "consumer_id": "vela_example-sdjl",
          "recipient_user_ids": [
              "vela_example_20492",
              "vela_example-2k23"
          ]
      },
      "message_thread_id": 8005,
      "message_type": "CHAT_MESSAGE",
      "reader_type": "ALL",
      "sender_user_id": "vela_example_jsjkd2",
      "status": "ACTIVE",
      "updated_at": "2019-04-24T15:42:52Z"
  }
  ```

### Event-type 13

  ```json
  {
      "additional_data": null,
      "attachment_id": null,
      "chat_message_id": 979532,
      "content": "gphcn",
      "created_at": "2019-03-29T02:31:26Z",
      "message_thread": {
          "confidential": true,
          "consumer_id": "V00007413040939381668",
          "recipient_user_ids": [
              "V01237413010002483668",
              "V01231233020142083668",
              "V01231233040123483668"
          ]
      },
      "message_thread_id": 999936,
      "message_type": "CHAT_MESSAGE",
      "reader_type": "ALL",
      "sender_user_id": "V00039413010092883668",
      "status": "DELETED",
      "updated_at": "2019-03-29T02:31:30Z"
  }
  ```

### Event-types 14-15-16

  ```json
  {
      "alert_status": "OPEN",
      "alert_template": "PastDueQuestionnaires",
      "alert_type": "MissedCheck",
      "associated_object": {
          "associated_object_internal_id": 19012523,
          "associated_object_type": "QuestionnaireAssignment"
      },
      "care_team_id": {
          "long": 99999
      },
      "contents": {
          "content": "Just a gentle reminder.",
          "for_date": "2019-09-18",
          "subject": "Missing INCIDENT"
      },
      "created_at": "2019-09-21T12:01:21Z",
      "created_by": null,
      "email_recipient_user_ids": [],
      "event_timestamp": "2019-09-21T12:01:21Z",
      "from_user_id": "V00999927050000000004",
      "id": 13455448,
      "notified": false,
      "push_recipient_user_ids": [],
      "reference_user_id": "V00000000990000000004",
      "sms_recipient_user_ids": [],
      "to_user_ids": [
          "V00000999990000000004"
      ],
      "updated_at": "2019-09-21T12:01:21Z",
      "updated_by": null,
      "visible_to_non_readers": false
  }
  ```

### Event-types 17-18-19

  ```json
  {
      "created_at": "2019-09-15T21:54:00Z",
      "created_by": "V00099999970000138326",
      "data_tag": null,
      "id": 142240,
      "label": {
          "en": "Questionnaire_bywejtjx_1568584440518"
      },
      "nodes": [],
      "updated_at": "2019-09-15T21:54:00Z",
      "updated_by": "V00012787970000138326"
  }
  ```

### Event-types 20-21-22-23

  ```json
  {
      "answers": [
          {
              "answer_internal_id": 99999,
              "created_at": "2019-04-24T20:35:59Z",
              "created_by": "V09999999990000000009",
              "question": {
                  "data_tag": {
                      "string": "q4"
                  },
                  "label": "feedback",
                  "question_type": "OPEN",
                  "questionnaire_node_internal_id": 99999,
                  "text": {
                      "en": "Please let us know any feedback about your experience or how we could further improve the overall support experience"
                  }
              },
              "response": null,
              "updated_at": "2019-04-24T20:35:59Z",
              "updated_by": "V00000099990000000009"
          },
          {
              "answer_internal_id": 23347,
              "created_at": "2019-04-24T20:35:59Z",
              "created_by": "V00000099990000000009",
              "question": {
                  "data_tag": {
                      "string": "q3"
                  },
                  "label": "On a scale of 1-10 how likely would would you recommend Vela Support to your friends or family.\n 10 Being most likely and 1 being least likely to recommend.",
                  "question_type": "CHOICE",
                  "questionnaire_node_internal_id": 99999,
                  "text": {
                      "en": "On a scale of 1-10 how likely would would you recommend Vela Support to your friends or family.\n 10 Being most likely and 1 being least likely to recommend."
                  }
              },
              "response": {
                  "string": "10"
              },
              "updated_at": "2019-04-24T20:35:59Z",
              "updated_by": "V00000099990000000009"
          },
          {
              "answer_internal_id": 99999,
              "created_at": "2019-04-24T20:35:59Z",
              "created_by": "V00000099990000000009",
              "question": {
                  "data_tag": {
                      "string": "q1"
                  },
                  "label": "Our records show that you have recently contacted Vela Support. Could you please take a couple of moments to let us know how we did?",
                  "question_type": "CHOICE",
                  "questionnaire_node_internal_id": 99999,
                  "text": {
                      "en": "Our records show that you have recently contacted Vela Support. Could you please take a couple of moments to let us know how we did?"
                  }
              },
              "response": {
                  "string": "ok"
              },
              "updated_at": "2019-04-24T20:35:59Z",
              "updated_by": "V00000099990000000009"
          }
      ],
      "associated_with_id": "V00000099990000000009",
      "associated_with_type": "USER",
      "created_at": "2019-04-24T20:04:57Z",
      "created_by": "V00000000990000000009",
      "expire_at": "2019-05-10T20:04:52Z",
      "expired": false,
      "overdue": false,
      "overdue_at": null,
      "questionnaire_assignment_id": 9999999,
      "questionnaire_assignment_schedule_id": null,
      "questionnaire_data_tag": null,
      "questionnaire_id": 99999,
      "questionnaire_label": "Support Survey",
      "respondents": [
          {
              "respondent_id": "V00000099990000000009",
              "respondent_type": "USER"
          }
      ],
      "secondary_respondents": [],
      "start_at": "2019-04-24T20:04:49Z",
      "status": "STARTED",
      "submitted_at": null,
      "submitted_by": null,
      "updated_at": "2019-04-24T20:35:59Z",
      "updated_by": "V00000099990000000009",
      "watchers": [
          {
              "watcher_id": "V00000099990000000009",
              "watcher_type": "USER"
          }
      ]
  }
  ```

### Event-types 24-25-26-27-28-29

  ```json
  {
      "created_at": "2021-09-24T18:15:35Z",
      "message_id": 1,
      "message_subject": "test subject",
      "message_type": "EMAIL",
      "url_clicked": "test link",
      "user_ids": [2019906]
  }
  ```

### Event-type 30
```json
{
    "chat_message_id": 1,
    "reader_user_id": "V00001799890000039598",
    "care_team_id": 5,
    "read_at": "2021-09-24T18:15:35Z"
}
```

### Event-type 31
```json
{
    "activity_data": {
        "chat_message_id": 9499581,
        "current_user_id": "V00001661540000006293",
        "message_thread_id": 3386641
    },
    "activity_target": { "file_id": null, "url": "https://example.com" },
    "activity_time": "2022-01-20T14:28:31Z",
    "activity_type": "URL_CLICKED",
    "client_app_name": "VELA_PRO_WEB",
    "user_id": "V00001661540000006293",
    "username": "example_cm"
}
```

### Event-types 32-33-34

  ```json
    {
            "automated": false,
            "care_team_id": 323576,
            "created_at": "2022-06-07T17:44:15Z",
            "created_by": "V00001799890000039598",
            "id": 140383,
            "item_statuses": [
                {
                    "status": "IN_PROGRESS",
                    "topic_node_id": 793478
                },
                {
                    "status": "COMPLETE",
                    "topic_node_id": 793477
                }
            ],
            "resume_at": null,
            "status": "IN_PROGRESS",
            "topic_id": 793474,
            "topic_identifier": "12",
            "updated_at": "2022-06-07T17:44:51Z",
            "updated_by": "V00001799890000039598"
    }
  ```

  ### Event-types 35

  ```json
  {
      "client_application": "VELA_PRO_WEB",
      "user_id": "vela_example_347",
      "username": "example_cm",
      "access_granted_flag": "true",
      "recorded_at": "2023-04-24T15:15:39Z"
  }
  ```
