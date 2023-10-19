# Resource Availability Zone

Resource Availability Zone is a provider assigned identifier for a physically separated and isolated area within a Resource Region that provides high availability and fault tolerance. Resource Availability Zone is commonly used for scenarios like analyzing cross-zone data transfer cost and usage based on where resources are deployed.

The ResourceAvailabilityZone column SHOULD be present in the billing data. This column MUST be of type String and MAY contain null values.

## Column ID

ResourceAvailabilityZone

## Display name

Resource Availability Zone

## Description

A provider assigned identifier for a physically separated and isolated area within a Resource Region that provides high availability and fault tolerance.

## Content constraints

| Constraint      | Value            |
|:----------------|:-----------------|
| Column required | False            |
| Data type       | String           |
| Allows nulls    | True             |
| Value format    | \<not specified> |

## Introduced (version)

0.5
