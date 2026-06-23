---
name: salesforce-queries
description: >-
  Query the CipherHealth Salesforce org via MCP for accounts, opportunities,
  contacts, tasks, and meeting briefs. Use when the user asks about CRM data,
  account status, pipeline, contacts, activity history, or pre-meeting briefs.
---

# CipherHealth Salesforce queries

Use the **Salesforce** MCP server (`soqlQuery`, `find`, `getObjectSchema`, `getUserInfo`).

If tools are missing or auth fails, tell the user to open **Settings → Tools & MCP → Salesforce → Connect** and complete OAuth. Do not guess CRM data.

## Scope (CipherHealth org rules)

**Allowed:** Account, Opportunity, Contact, Lead, Campaign, Task, Event, Product-related objects.

**Never query:** Cases, support tickets, clinical-outcome objects, or anything with PHI.

## Defensive querying

- Confirm custom fields with `getObjectSchema` when unsure.
- If SOQL fails on an unknown field, drop it and retry.
- Always use `WHERE` filters and `LIMIT` (default 50 unless the user needs more).
- Chunk `IN` lists to ~200 IDs.

## Account lookup

Start with `find` when the user gives a fuzzy name:

```
FIND {Acme Health} IN NAME FIELDS RETURNING Account(Id, Name, Type, Owner.Name, LastActivityDate)
```

Or SOQL:

```sql
SELECT Id, Name, Type, Owner.Name, LastActivityDate, BillingState
FROM Account
WHERE Name LIKE '%SearchTerm%'
LIMIT 10
```

## Meeting brief workflow

When prepping for a customer meeting, run these in order:

1. **Account** — type, owner, last activity
2. **Open opportunities** on that account (or parent account if hospital vs physician group)
3. **Key contacts** — executives, nursing, pharmacy, CMIO
4. **Recent tasks** — last 10–15 activities (Gong emails, calls)

```sql
SELECT Id, Name, StageName, Amount, CloseDate, Probability, Type, NextStep, Owner.Name
FROM Opportunity
WHERE AccountId = 'ACCOUNT_ID' AND IsClosed = false
ORDER BY Amount DESC NULLS LAST
```

```sql
SELECT Id, Name, Title, Email, Phone
FROM Contact
WHERE AccountId = 'ACCOUNT_ID'
ORDER BY LastModifiedDate DESC
LIMIT 20
```

```sql
SELECT Id, Subject, ActivityDate, Status, Description
FROM Task
WHERE AccountId = 'ACCOUNT_ID'
ORDER BY ActivityDate DESC
LIMIT 15
```

Summarize for executives: relationship status, live products/programs, open pipeline, last touch, key contacts, 3–4 talking points. Flag stale CRM (no activity in 90+ days).

## Standard query patterns

See [references/salesforce_queries.md](references/salesforce_queries.md) for customer accounts, target prospects, open pipeline, and key contacts.

## Org notes

- `Target_Account__c` is text `'true'`/`'false'`, not boolean.
- UCI may appear as **UCI Health Physicians** (physician group) or **University of California Irvine Medical Center** (hospital) under **University of California Health** parent.
- Account `Type` can be wrong vs actual customer status — corroborate with opportunities and task history.
