# entitlements-manager

This project outlines a practical approach to generically managing user permissions on any given platform

# Concepts

## Entity

A _noun_ that users can manipulate, this forms the basis for entitlements management in that ultimately, all permissions are reduced to the form "subject X can do verb Y on entity Z". Entities have the following schema:

```yaml
entityType: Article
entityId: 12
property1: some value
property2: some value
entitlements:
 view: 
  - user:john
  - group:premium_readers
  - group:acme_corp_employees
 edit:
  - user:ceo_guy
  - group:senior_editors
```

## User

A user is represented by the following schema

```yaml
entityType: User
entityId: john
tokens:
 - group:premium_readers
entitlements:
 view:
  - user:john
  - group:administrators
  - group:premium_users
 edit:
  - group:administrators
  - user:john
```

## Groups

A group is a special entity type - which can be added/removed to `entitlements` of any other entity. It has the schema:

```yaml
entityType: Group
entityId: premium_readers
name: Premium Readers
description: |
  Subscribers to our premium service
entitlements:
  view:
   - group:administrators
  add_member:
   - group:administrators
   - machine_user:subscription_service_bot
  remove_member:
   - group:administrators
   - machine_user:subscription_service_bot
  edit:
   - group:administrators
   - user:ceo_guy
```
