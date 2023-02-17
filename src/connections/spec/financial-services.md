---
title: 'Spec: Financial Services'
---

This guide explains how Financial Service companies should send core user and account data to Segment.

## Overview

Most Financial Service companies have a few common, core events for users, accounts and transactions. We understand that account hierarchies can be unique and complex, but by following this spec you can take advantage of account-based tools on Segment platform, and Financial Service data products by Segment.


## Events

The Financial Service category has the following semantic events:

* [Account Created](#account-created)
* [Account Closed](#account-closed)
* [Signed In](#signed-in)
* [Signed Out](#signed-out)
* [Invite Sent](#invite-sent)
* [Account Added User](#account-added-user)
* [Account Removed User](#account-removed-user)
* [Adverse Action Delivered](#adverse-action)
* [Agreement Drawn](#agreement-drawn)
* [Agreement Executed](#agreement-executed)
* [Agreement Exited](#agreement-exited)
* [Application Delivered](#application-delivered)
* [Application Signed](#application-signed)
* [Application Revised](#application-revised)
* [Application Withdrawn](#application-withdrawn)
* [Closing Scheduled](#closing-scheduled)
* [Credit Pulled](#credit-pulled)
* [Disclosure Issued](#disclosure-issued)
* [Document Received](#document-received)
* [Document Requested](#document-requested)
* [Escrow Funded](#escrow-funded)
* [Fee Applied](#fee-applied)
* [Funds Disbursed](#funds-disbursed)
* [Offer Presented](#offer-presented)
* [Offer Accepted](#offer-accepted)
* [Offer Rejected](#offer-rejected)
* [Payment Received](#payment-recieved)
* [Payment Returned](#payment-returned)
* [Recording Completed](#recording-completed)
* [Refund Approved](#refund-approved)
* [Refund Denied](#refund-denied)
* [Refund Requested](#refund-requested)
* [Service Ordered](#service-ordered)
* [Service Returned](#service-returned)
* [Statement Created](#statement-created)
* [Statement Delivered](#statement-delivered)
* [Terms Delivered](#terms-delivered)
* [Terms Accepted](#terms-accepted)
* [Terms Declined](#terms-declined)
* [Transaction Cancelled](#transaction-cancelled)
* [Transaction Completed](#transaction-completed)
* [Underwriting Submitted](#underwriting-submitted)
* [Underwriting Responded](#underwriting-responded)

### Account Created

This event should be sent when a new account is created.

#### Properties

This event supports the following semantic properties:

| Property          | Type   | Description                            |
| ----------------- | ------ | -------------------------------------- |
| `account_name`    | String | The name of the account being created. |
| `context.groupId` | String | The id of the account being created.   |



#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Created",
  "properties": {
    "account_name": "Initech"
  },
  "context": {
      "groupId": "acct_123"
      }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Created",
  "properties": {
    "account_name": "Initech"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```

### Account Closed

This event should be sent when an account is closed/no longer valid.  

> **Good to know**: This is equivilant to Account Deleted in other Segment specs, but fully removing accounts is not allowed in regulated industries like health care and finance.

#### Properties

This event supports the following semantic properties:

| Property          | Type   | Description                            |
| ----------------- | ------ | -------------------------------------- |
| `account_name`    | String | The name of the account being deleted. |
| `context.groupId` | String | The id of the account being deleted.   |

#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Deleted",
  "properties": {
    "account_name": "Initech"
  },
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Deleted",
  "properties": {
    "account_name": "Initech"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```


### Signed In

This event should be sent when a user signs in to your service.

> success ""
> **Good to know**: Segment's best practice is to use an "Object-Action" naming convention, which in this case would be "User Signed In". However, because in the B2B case this may not be a specific user, we omit that noun in our example. You may include or omit it as needed for your implementation.

#### Properties

This event supports the following semantic properties:

| Property          | Type   | Description                                                |
| ----------------- | ------ | ---------------------------------------------------------- |
| `username`        | String | The username of the user signing in.                       |
| `context.groupId` | String | The id of the account associated with the user signing in. |


#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Signed In",
  "properties": {
    "username": "pgibbons"
  },
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```json
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Signed In",
  "properties": {
    "username": "pgibbons"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```

### Signed Out

This event should be sent when a user signs out for your service. You should also call [`analytics.reset()`](/docs/connections/sources/catalog/libraries/website/javascript/#reset-or-logout) to refresh the cookie when a Signed Out event occurs.

> success ""
> **Good to know**: Segment's best practice is to use an "Object-Action" naming convention, which in this case would be "User Signed Out". However, because in the B2B case this may not be a specific user, we omit that noun in our example. You may include or omit it as needed for your implementation.

#### Properties

This event supports the following semantic properties:

| Property          | Type   | Description                                                 |
| ----------------- | ------ | ----------------------------------------------------------- |
| `username`        | String | The username of the user signing out.                       |
| `context.groupId` | String | The id of the account associated with the user signing out. |

#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Signed Out",
  "properties": {
    "username": "pgibbons"
  },
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Signed Out",
  "properties": {
    "username": "pgibbons"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```

### Invite Sent

This event should be sent when a user invites another user.

#### Properties

This event supports the following semantic properties:

| Property             | Type   | Description                                               |
| -------------------- | ------ | --------------------------------------------------------- |
| `invitee_email`      | String | The email address of the person receiving the invite.     |
| `invitee_first_name` | String | The first name of the person receiving the invite.        |
| `invitee_last_name`  | String | The last name of the person receiving the invite.         |
| `invitee_role`       | String | The permission group for the person receiving the invite. |
| `context.groupId`    | String | The id of the account the person is being invited to.     |

#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Invite Sent",
  "properties": {
    "invitee_email": "pgibbons@example.com",
    "invitee_first_name": "Peter",
    "invitee_last_name": "Gibbons",
    "invitee_role": "Owner"
  },
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Invite Sent",
  "properties": {
    "invitee_email": "pgibbons@example.com",
    "invitee_first_name": "Peter",
    "invitee_last_name": "Gibbons",
    "invitee_role": "Owner"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```

### Account Added User

This event should be sent when a user is added to a group.

#### Properties

This event supports the following semantic properties:

| Property          | Type   | Description                                         |
| ----------------- | ------ | --------------------------------------------------- |
| `role`            | String | The permission group for this user in this account. |
| `context.groupId` | String | The id of the account the user is being added to.   |

#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Added User",
  "properties": {
    "role": "Owner"
  },
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Added User",
  "properties": {
    "role": "Owner"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```

### Account Removed User

This event should be sent when a user is removed from a group or account.

#### Properties

This event supports the following semantic properties:

| Property          | Type   | Description                                           |
| ----------------- | ------ | ----------------------------------------------------- |
| `context.groupId` | String | The id of the account the user is being removed from. |

#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Removed User",
  "properties": {},
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Account Removed User",
  "properties": {},
  "context": {
    "groupId": "acct_123"
  }
}
```

### Adverse Action Delivered

This event should be sent when an application results in an adverse action that requires notification for legal purposes.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `locality` | Object   | The locality of the applicant. |
| `loss_reason`   | String   | Reason for the adverse action.   |
| `loss_type`  | String | Additional details of related to the action.                            |
| `context.groupId`  | String | The id of the account the action is associated with.            |

#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Trial Started",
  "properties": {
    "trial_start_date": "2018-08-28T04:09:47Z",
    "trial_end_date": "2018-09-20T04:09:47Z",
    "trial_plan_name": "Business"
  },
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Trial Started",
  "properties": {
    "trial_start_date": "2018-08-28T04:09:47Z",
    "trial_end_date": "2018-09-20T04:09:47Z",
    "trial_plan_name": "Business"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```

### Agreement Drawn

This event should be sent when a new agreement or contract is drawn up.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `agreement_start_date` | Date   | The date when the agreement starts. It is an ISO-8601 date string. |
| `agreement_end_date`   | Date   | The date when the agreement ends. It is an ISO-8601 date string.   |
| `agreement_type`  | String | The type of agreement.                            |
| `context.groupId`  | String | The id of the account the agreement is associated with.            |


#### Example

{% comment %} api-example '{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Agreement Drawn",
  "properties": {
    "trial_start_date": "2018-08-28T04:09:47Z",
    "trial_end_date": "2018-09-20T04:09:47Z",
    "trial_plan_name": "Business"
  },
  "context": {
    "groupId": "acct_123"
  }
}'}}} {% endcomment %}

```js
{
  "userId": "019mr8mf4r",
  "type": "track",
  "event": "Trial Ended",
  "properties": {
    "trial_start_date": "2018-08-28T04:09:47Z",
    "trial_end_date": "2018-09-20T04:09:47Z",
    "trial_plan_name": "Business"
  },
  "context": {
    "groupId": "acct_123"
  }
}
```

### Agreement Executed

This event should be sent when a new agreement or contract is signed.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `agreement_start_date` | Date   | The date when the agreement/contract starts. It is an ISO-8601 date string. |
| `agreement_end_date`   | Date   | The date when the agreement/contract ends. It is an ISO-8601 date string.   | 
| `executed_date`   | Date   | The date when the agreement/contract was officially signed. It is an ISO-8601 date string.   | 
| `agreement_id`   | String   | The ID of the document / agreement.   |                       |
| `context.groupId`  | String | The id of the account the agreement is associated with.            |


### Agreement Exited

This event should be sent when an existing agreement or contract is exited or completed.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `agreement_id`   | String   | The ID of the application (or opportunity).   |   
| `agreement_exited_date`   | Date   | The date when the agreement/contract was exited. It is an ISO-8601 date string.   | 
| `exit_reason`   | String   | The reason the agreement is ending.  |                       
| `context.groupId`  | String | The id of the account the agreement is associated with.            |

### Application Delivered

This event should be sent when a new application or contract is sent to user for signature.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `application_id`   | String   | The ID of the application (or opportunity).   |                    
| `date_delivered`   | Date   | The date when the application was presented to the user. It is an ISO-8601 date string.   | 
| `context.groupId`  | String | The id of the account the agreement is associated with.            |

### Application Signed

This event should be sent when a user returns a signed application or contract.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `application_id`   | String   | The ID of the application (or opportunity).   |             
| `date_signed`   | Date   | The date when the application was signed by the user. It is an ISO-8601 date string.   | 
| `context.groupId`  | String | The id of the account the agreement is associated with.            |

### Application Revised

This event should be sent when a user completes filling out a part/section of an application.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `application_id`   | String   | The document ID of the application (or opportunity).   |                       
| `application_type`   | String   | The product being applied for (i.e. auto loan, mortgage, etc.).   | 
| `section_updated`   | String   | The section of the application that was revised.   | 
| `context.groupId`  | String | The id of the account the application is associated with.            |

### Application Withdrawn

This event should be sent when an application or contract is cancelled by the user.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `application_id`   | String   | The ID of the application (or opportunity).   |                       
| `reason`   | String   | The reason the application is being closed.   |                       
| `context.groupId`  | String | The id of the account the agreement is associated with.            |

### Closing Scheduled

This event should be sent when a Closing meeting is scheduled.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `scheduled_time`   | DateTime   | The date and time the closing meeting is scheduled.   |  
| `location`   | String   | The location of the closing meeting.   |  
| `agreement_id`   | String   | The ID of the agreement to be executed at the closing.   |  
| `context.groupId`  | String | The id of the account the closing is associated with.            |

### Credit Pulled

This event should be sent when a user's credit is pulled from a credit bureau.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `type`   | String   | The type of credit pull initiated (soft, hard).   |   
| `credit_bureau`   | String   | The name of the credit bureau or source of the credit report   |   
| `transaction_id`   | String   | The transaction ID provided by the credit service endpoint.   |  
| `score`   | Number   | The numeric credit score.   | 
| `score_provider`   | String   |  FICO&reg; or Vantage&reg;  | 
| `score_type`   | String   | The type of score returned.   | 
| `scores`   | Object   | If multiple reports are requested, the response is an object array.   | 
| `context.groupId`  | String | The id of the account the agreement is associated with.            |

### Disclosure Issued

This event should be sent when a disclosure document is sent to a user.

#### Properties

This event supports the following semantic properties:


### Document Requested

This event should be sent when a document is requested from a user.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `document_id`   | String/Number   | The ID assigned to the document   |   
| `document_type`   | String  | The type of document being requested.  |  
| `due_date`   | Date  | Date the document must be returned.   |                                            


### Document Received

This event should be sent when a document is received from a user.

#### Properties

This event supports the following semantic properties:

| Property           | Type   | Description                                                    |
| ------------------ | ------ | -------------------------------------------------------------- |
| `document_id`   | String/Number   | The ID assigned to the document   |   
| `document_type`   | String  | The type of document being requested.  |  
| `document`   | String  | The URL of the document  | 
| `remaining_docs_requested`   | Number  | The number of additional documents that have been requested.  | 

### Escrow Funded

This event should be sent when funds are sent to an escrow account.

#### Properties

This event supports the following semantic properties:


### Fee Applied

This event should be sent when a fee is charged to an account.

#### Properties

This event supports the following semantic properties:


### Funds Disbursed

This event should be sent when a funds are disbursed to a user or their proxy either directly or from an escrow account.

#### Properties

This event supports the following semantic properties:


### Offer Presented

This event should be sent when an offer is presented to a user.

#### Properties

This event supports the following semantic properties:


### Offer Accepted

This event should be sent when an offer is presented to a user.

#### Properties

This event supports the following semantic properties:


### Offer Rejected

This event should be sent when an offer is presented to a user.

#### Properties

This event supports the following semantic properties:


### Payment Received

This event should be sent when a payment is received from a user/proxy.

#### Properties

This event supports the following semantic properties:


### Payment Returned

This event should be sent when a payment is returned due to error (NSF, etc.).

#### Properties

This event supports the following semantic properties:


### Recording Completed

This event should be sent when a recording of a transaction with a government entity has been finalized, typically with a real estate transaction.

#### Properties

This event supports the following semantic properties:


### Refund Approved

This event should be sent when a refund requested by a user has been approved.

#### Properties

This event supports the following semantic properties:


### Refund Requested

This event should be sent when a refund is requested by a user.

#### Properties

This event supports the following semantic properties:


### Refund Denied

This event should be sent when a refund requested by a user has been denied.

#### Properties

This event supports the following semantic properties:


### Service Ordered

This event should be sent when services are ordered as part of an agreement.  This is typically part of a real estate transaction that requires appraisal and title be collected from a 3rd party.

#### Properties

This event supports the following semantic properties:


### Service Returned

This event should be sent when an ordered service has returned to necessary materials.

#### Properties

This event supports the following semantic properties:


### Statement Created

This event should be sent when an account statement has been generated.

#### Properties

This event supports the following semantic properties:


### Statement Delivered

This event should be sent when an account statement has been delivered to the user.

#### Properties

This event supports the following semantic properties:


### Terms Delivered

This event should be sent when an agreement or contract terms have been presented to the user.

#### Properties

This event supports the following semantic properties:


### Terms Accepted

This event should be sent when a user has accepted the terms of an agreement or contract.

#### Properties

This event supports the following semantic properties:


### Terms Declined

This event should be sent when a user has declined to accept the terms of an agreement or contract.

#### Properties

This event supports the following semantic properties:


### Transaction Cancelled

This event should be sent when a transaction on an account is cancelled or rolled back.

#### Properties

This event supports the following semantic properties:


### Transaction Completed

This event should be sent when a transaction on an account has finalized.

#### Properties

This event supports the following semantic properties:


### Underwriting Submitted

This event should be sent when a file is submitted to an underwriter for approval.  Typically occurs in real estate and insurance transactions.

#### Properties

This event supports the following semantic properties:


### Underwriting Responded

This event should be sent when a file is returned from the underwriter.  Typically occurs in real estate and insurance transactions.

#### Properties

This event supports the following semantic properties:
