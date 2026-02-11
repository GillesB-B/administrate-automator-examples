# Merge Accounts

Version: 1.0.0  
Last Updated: 2026-02-11

---

## Problem

Duplicate accounts in Administrate create reporting inconsistencies, fragmented financial history, and operational confusion. 

When the same organization exists more than once, contacts, bookings, and financial records may be split across records. Manually resolving this is time-consuming and prone to error.

---

## Solution

This workflow provides a guided web form that allows users to merge one account into another safely.

The user selects:
- A **From Account** (the account to be merged)
- A **To Account** (the account that will remain)

The workflow:
1. Validates both accounts exist.
2. Confirms the merge action with the user.
3. Executes the merge via the Administrate API.
4. Displays a clear success or failure message.

This process is irreversible.

---

## Features

- Simple web-based form interface
- Validates both account IDs before merging
- Explicit confirmation step before execution
- Clear success and failure messaging
- Prevents merge if either account does not exist
- Displays API error messages when merge fails

---

## Setup Instructions

### Prerequisites

- Active n8n instance
- Administrate OAuth2 API credentials configured in n8n
- Permission to merge accounts in Administrate
- Access to publish a link internally (e.g., homepage announcement)

---

### Installation

1. Import the workflow JSON into n8n.
2. Open the workflow.
3. Configure Administrate OAuth2 credentials on all API request steps.
4. Activate the workflow.
5. Copy the **Production URL** from the form trigger.
6. Publish the URL internally (e.g., homepage announcement or internal bookmark).

---

### Configuration

#### Administrate OAuth2 Credentials

This workflow requires:
- Access to the Administrate GraphQL API
- Permission to:
  - Read account records
  - Perform account merge operations

Ensure the selected OAuth2 credential has sufficient permissions.

#### Web Form Access

Anyone with the production URL can access and use this tool.

If restricted access is required, additional access controls must be implemented outside this workflow.

---

## Testing

1. Activate the workflow.
2. Open the production form URL.
3. Enter:
   - A valid **From Account ID**
   - A valid **To Account ID**
4. Confirm the merge when prompted.
5. Verify:
   - Success message appears.
   - The merged account reflects consolidated data inside Administrate.

To test failure scenarios:
- Enter a non-existent Account ID.
- Attempt a merge that violates business rules (if applicable).

---

## Usage

### Triggering the Workflow

This workflow is triggered by submitting the web form.

Required fields:

- **From Account ID** (numeric)
- **To Account ID** (numeric)

Important:
- Use the **Account ID**, not a Contact ID.
- The “From Account” will be merged into the “To Account”.
- This action cannot be undone.

---

## How It Works

1. User submits From and To Account IDs.
2. The workflow verifies both accounts exist.
3. The user is shown a confirmation screen displaying both account names.
4. Upon confirmation, the merge operation is executed.
5. The system evaluates the result.
6. A success or failure message is displayed.

---

## Response Flow

### Account Not Found

If either Account ID does not exist:
- The workflow stops.
- A message is shown identifying the account that could not be found.
- The user is directed to Administrate Support if needed.

---

### Merge Success

If the merge completes without errors:
- A success message is displayed.
- The user may close the window.

---

### Merge Failure

If the merge API returns an error:
- The specific error message is displayed.
- The user is directed to Administrate Support.

---

## Troubleshooting

### “Account not found”

Cause:
- Incorrect Account ID entered.
- Contact ID used instead of Account ID.

Resolution:
- Confirm the correct Account ID in Administrate.
- Retry the merge.

---

### Merge fails after confirmation

Cause:
- Business rule restriction in Administrate.
- Insufficient permissions.
- Invalid account state for merging.

Resolution:
- Review the displayed error message.
- Confirm API permissions.
- Contact Administrate Support if required.

---

## API Permissions Required

The connected Administrate OAuth2 application must have permission to:

- Read account records
- Execute account merge mutations

If merge attempts fail due to authorization errors, review OAuth2 scopes and account permissions.
