# Pricing Unit

The Pricing Unit represents a provider specified pricing measurement unit, which forms the foundation for determining unit prices of utilizing a particular resource and/or service. Common examples include the number of hours a compute appliance was running for a given period, the number of gigabytes * the number of hours (gigabyte-hours) for a storage appliance, or a cumulative count of requests for a network appliance or API service. For certain services providers can choose block pricing i.e., million requests as a base unit.
PricingUnit is complementary to and describes how [QuantityInPricingUnit](#quantityinpricingunit) is measured.

The PricingUnit column MUST be present in the billing data. This column MUST be of type String. It MUST NOT contain null if [QuantityInPricingUnit](#quantityinpricingunit) is not null. The PricingUnit value MUST match what is shown on the invoice if a pricing unit is present on the invoice.

## Column ID

PricingUnit

## Display name

Pricing Unit

## Description

Represents a provider specified pricing measurement unit, which forms the foundation for determining unit prices of utilizing a particular resource and/or service.

## Content constraints

| Constraint      | Value           |
|-----------------|-----------------|
| Column required | True            |
| Data type       | String          |
| Allows nulls    | True            |
| Value format    | \<not specified> |

## Introduced (version)

1.0