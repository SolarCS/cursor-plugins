# Salesforce queries — CipherHealth org

Verified against the CipherHealth org (API v64). Use with the Salesforce MCP `soqlQuery` tool.

## 1. Customer accounts

```sql
SELECT Id, Name, Website, Website_Domain__c, Aliases__c, Top_Level_Parent_Name__c,
       BillingState, Region__c, Type, Account_Tier__c, Customer_Segmentation__c,
       Products__c, EMR_Vendor__c, Account_Health__c, Churn_Forecast_Category__c,
       Open_Opportunities__c, Total_Account_Pipeline_Dollars__c,
       What_to_sell_next__c, Estimated_Expansion_Amount__c, Pain_Points__c,
       Last_Sales_Meeting_Date__c, Owner.Name
FROM Account
WHERE Is_Customer__c = true
ORDER BY Total_Account_Pipeline_Dollars__c DESC NULLS LAST
LIMIT 100
```

## 2. Target / key prospects

```sql
SELECT Id, Name, Website, Website_Domain__c, Aliases__c, Top_Level_Parent_Name__c,
       BillingState, Region__c, Type, Account_Tier__c, Target_Account__c, Key_Account__c,
       EMR_Vendor__c, Open_Opportunities__c, Total_Account_Pipeline_Dollars__c,
       Patient_Engagement_Intent_Score__c, Care_Coordination_Intent_Score__c,
       Readmissions_Intent_Score__c, Owner.Name
FROM Account
WHERE Is_Customer__c = false
  AND (Target_Account__c = 'true' OR Key_Account__c = true)
ORDER BY Total_Account_Pipeline_Dollars__c DESC NULLS LAST
LIMIT 100
```

## 3. Open opportunities

```sql
SELECT Id, Name, AccountId, Account.Name, StageName, Amount, CloseDate, Type,
       Probability, NextStep, Owner.Name
FROM Opportunity
WHERE IsClosed = false
ORDER BY Amount DESC NULLS LAST
LIMIT 100
```

## 4. Key contacts (chunk AccountIds)

```sql
SELECT Id, Name, Title, Email, AccountId, Account.Name
FROM Contact
WHERE AccountId IN ('001...', '001...')
  AND (Title LIKE '%Chief%' OR Title LIKE '%VP%'
       OR Title LIKE '%Director%' OR Title LIKE '%Nurs%' OR Title LIKE '%Experience%')
LIMIT 200
```

## 5. Leads (optional)

```sql
SELECT Id, Name, Company, Title, Email, Status, State
FROM Lead
WHERE Status != 'Disqualified' AND Company != null
LIMIT 100
```
