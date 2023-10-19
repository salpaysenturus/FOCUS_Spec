# Resource Region

A Resource Region is a provider assigned identifier for an isolated geographic area where a resource is provisioned in. Resource Region is commonly used for scenarios like analyzing cost and prices based on where resources are deployed.

The ResourceRegion column MUST be present in the billing data. This column MUST be of type String and MUST NOT contain null values. ResourceRegion values MUST be consistent within the provider and MUST be the same values used to indicate the region when provisioning or purchasing the resource.

## Column ID

ResourceRegion

## Display name

Resource Region

## Description

Isolated geographic area where a resource is provisioned in and/or a service is provided from.

## Content constraints

| Constraint      | Value           |
|-----------------|-----------------|
| Column required | True            |
| Data type       | String          |
| Allows nulls    | False           |
| Value format    | \<not specified> |

## Introduced (version)

0.5
