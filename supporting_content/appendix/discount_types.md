# Discount Types

Providers offer various discounting schemes for their service offerings. These discounts typically fall into common types such as:

* Commitment-based discounts
* Tier-based discounts
* Negotiated discounts
* Promotional discounts
* Partnership-based discounts

## Commitment-based discounts

Notes:

* Usage-based commitment discounts
* Spend-based commitment discounts

## Tier-based discounts

* RI Volume Discounts?

## Negotiated discounts

TBD

## Promotional discounts

* Free Trial

## Partnership-based discounts

* Private Rate Discounts
* Enterprise Discount Program discounts
* RESELLER_MARGIN


# Links to documentation

* AWS
  * Bundled discounts - https://aws.amazon.com/blogs/aws-cloud-financial-management/bundled-discounts-in-aws-cost-and-usage-report/

* GCP
  * Credit types - https://cloud.google.com/billing/docs/how-to/export-data-bigquery-tables/standard-usage#standard-usage-cost-data-schema

# Discussion / Scratch space

* AWS discount types include:
  * DiscountedUsage - discounts covered by Reserved Instances
  * SavingsPlanCoveredUsage - discounts covered by SavingsPlans
  * EdpDiscount - Enterprise Discount Program
  * SppDiscount - Solutions Provider Program
  * RiVolumeDiscount
  * BundledDiscount - discounted usage on a specific product/service based on the usage of another product/service.

* GCP discount types include:
  * DISCOUNT - credits earned after a contractual spending threshold is reached.
  * COMMITTED_USAGE_DISCOUNT - resource-based commitment discounts.
  * COMMITTED_USAGE_DISCOUNT_DOLLAR_BASE - Spend-based commitment discounts.
  * SUSTAINED_USAGE_DISCOUNT - automatic discount earned for prolonged usage.
  * FREE_TIER - free resource usage up to specified limits.
  * PROMOTION - includes free tial, marketing campaign credits, or other grants to use GCP.
  * RESELLER_MARGIN - indicates the Reseller Program Discounts earned on every eligible line item.
  * SUBSCRIPTION_BENEFIT - credits earned by purchasing long-term subscriptions to services in exchange for discounts.

* Where does spot instance usage-based discount fall? Should there be a **Usage-based discounts** type?

* Where does GCP's sustained usage discount fall? Maybe the same as spot instance, in which case, **Usage-based discounts**?
