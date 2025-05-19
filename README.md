# SQL Analysis: Email Delivery Metrics by Account and Month

This SQL project calculates detailed **email delivery metrics** for each account on a monthly basis. It determines how active each account is in terms of email engagement and tracks the timeline of email interactions.

## Purpose

The query provides monthly statistics for email activity, including:
- The **percentage of total emails** sent to each account
- The **first and last date** an email was sent to an account in each month

## Data Sources

The query uses the following tables from the `data-analytics-mate.DA` dataset:

- `email_sent`: Contains records of emails sent, including `sent_date` and `id_account`
- `account_session`: Links accounts to session IDs
- `session`: Contains session-level metadata, including base session dates

## Query Breakdown

The logic is split into two main Common Table Expressions (CTEs):

### 1. `email_metrics`

For each account and month:
- Calculates the **number of emails** sent (`msg_cnt`)
- Extracts the **first and last email send dates**
- Converts relative send dates into full dates using `DATE_ADD`

### 2. `final_email_metrics`

For each month:
- Aggregates the **total number of emails sent** to all accounts

### Final SELECT

Combines both CTEs to compute:
- **Email share**: The percentage of monthly emails sent to each account
- **First and last sent dates** for each account that received emails during the month

## Output Columns

- `sent_month`: The calendar month (formatted as `YYYY-MM-01`)
- `id_account`: Unique identifier of the recipient account
- `sent_msg_percent_from_this_month`: The percentage of emails sent to this account in the given month
- `first_sent_date`: Date of the first email sent in that month
- `last_sent_date`: Date of the last email sent in that month
