# Service Name

A service represents an offering that can be purchased from a provider (e.g., cloud virtual machine, SaaS database, professional services from a systems integrator). A service offering can include various types of usage or other charges. For example, a cloud database service may include compute, storage, and networking charges.

The Service Name is a display name for the offering that was purchased. The Service Name is commonly used for scenarios like analyzing aggregate cost trends over time and filtering data to investigate anomalies.

The ServiceName column MUST be present in the cost data. This column MUST be of type String and MUST NOT contain null values.

## Column ID

ServiceName

## Display Name

Service Name

## Description

An offering that can be purchased from a provider (e.g., cloud virtual machine, SaaS database, professional services from a systems integrator).

## Content Constraints

| Constraint      | Value            |
| :-------------- | :--------------- |
| Column required | True             |
| Data type       | String           |
| Allows nulls    | False            |
| Value format    | \<not specified> |

## Introduced (version)

0.5
