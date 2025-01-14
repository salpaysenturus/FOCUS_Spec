# Quantity-Driven Pricing Strategies

## Introduction

Providers employ two primary approaches for pricing their offerings: flat-rate pricing and quantity-dependent pricing.

### Flat-Rate Pricing

With flat-rate pricing, each pricing unit is assigned a fixed price, regardless of the quantity being consumed. This pricing strategy is characterized by its simplicity, as customers are charged a consistent rate, making it easy to forecast costs.

### Quantity-Dependent Pricing (Usage-Dependent Pricing)

Quantity-dependent pricing, also referred to as usage-dependent pricing, takes into account the quantity and adjusts pricing accordingly. This approach involves configuring multiple price tiers, each defined by a specific quantity range and associated unit prices, such as ListUnitPrice, NegotiatedUnitPrice, BilledUnitPrice, etc.

Typically, higher usage tiers feature lower unit prices, offering users the advantage of reduced unit costs as their usage expands. Additionally, quantity-dependent pricing may include a **free-tier**, a special price tier designed for an introductory usage level.

Two common quantity-dependent pricing strategies are volume-based pricing and tier-based pricing. While both strategies reset the count of charged units at the beginning of each billing period, they differ in how charges are categorized into different price tiers:

* **volume-based pricing:** This strategy adjusts unit prices based on the total usage within a specific billing period, affecting all charges within it. Customers benefit from reduced unit costs as their overall usage increases.
* **tier-based pricing:** In tier-based pricing, unit prices change as the number of charged units increases. You are charged for the consumed quantity within each tier based on the associated unit price for each tier.

For better comprehension, please refer to the sample price-tiers configuration and UC scenarios, provided in Fictional Use Case scenarios.

## Example usage scenarios

### Fictional Use Case scenarios

#### Sample price-tiers configuration

|                            | Lower Tier | Higher Tier |
|:---------------------------|:-----------|:------------|
| List Unit Price            | 1          | 0.50        |
| Pricing currency           | USD        | USD         |
| Starting Range (inclusive) | 0          | 10GB        |
| Ending Range (exclusive)   | 10         | 100         |
| Pricing Unit               | 1GB        | 1GB         |
| Enterprise discount        | 10%        | 10%         |

#### UC scenarios for different (sub)types of pricing mechanisms

| Scenario | Description                                                                                                 |
|:---------|:------------------------------------------------------------------------------------------------------------|
| S-1      | Tier-based pricing: 12GB of usage falls into two different tiers, resulting in two separate charge records. |
| S-2      | Volume-based pricing: 12GB of usage falls into the highest tier, resulting in a single charge record.       |

#### Sample Billing data

| Scenario | QuantityInPricingUnit | PricingUnit | ListUnitPrice | NegotiatedUnitPrice | BilledUnitPrice | PricingCurrency | BillingCurrency | ListCost | BilledCost | EffectiveCost |
|:----|---:|:----|-----:|-----:|-----:|:----|:----|---:|----:|----:|
| S-1 | 10 | 1GB | 1    | 0.90 | 0.90 | USD | USD | 10 | 9   | 9   |
| S-1 | 2  | 1GB | 0.50 | 0.45 | 0.45 | USD | USD | 1  | 0.9 | 0.9 |
| S-2 | 12 | 1GB | 0.50 | 0.45 | 0.45 | USD | USD | 6  | 5.4 | 5.4 |

### Current values observed in billing data for various scenarios

| Provider  | Scenario                                                                           | ListUnitPrice Pattern                | BilledUnitPrice Pattern |
|:----------|:-----------------------------------------------------------------------------------|:-------------------------------------|:------------------------|
| AWS       | Flat-rate based pricing<br>SKU: E9YHNFENF4XQBZR6                                   | pricing/publicOnDemandRate: 0.000005 | *TODO: Add sample data* |
| AWS       | Quantity-dependent pricing<br> ??? *TODO: look for a higher tier sample*           | pricing/publicOnDemandRate: ??? *TODO: look for a higher tier sample* | *TODO: Add sample data* |
| GCP       | Flat-rate based pricing                                                            | Not available                        | *TODO: Add sample data* |
| GCP       | Quantity-dependent pricing                                                         | Not available                        | *TODO: Add sample data* |
| Microsoft | Flat-rate based pricing - PAYG<br>meterId: b9e5e77c-a0b3-4a2c-9b8b-57fa54f31c52    | PayGPrice: 0.00036                   | *TODO: Add sample data* |
| Microsoft | Flat-rate based pricing - CSP<br>meterId: b9e5e77c-a0b3-4a2c-9b8b-57fa54f31c52     | PayGPrice: 0.0003707                 | *TODO: Add sample data* |
| Microsoft | Quantity-dependent pricing - PAYG<br>meterId: 9995d93a-7d35-4d3f-9c69-7a7fea447ef4 | PayGPrice: 0.087                     | *TODO: Add sample data* |
| Microsoft | Quantity-dependent pricing - CSP<br>meterId: 9995d93a-7d35-4d3f-9c69-7a7fea447ef4  | PayGPrice: 0.087                     | *TODO: Add sample data* |
| OCI       | Flat-rate based pricing                                                            | Not available                        | *TODO: Add sample data* |
| OCI       | Quantity-dependent pricing                                                         | Not available                        | *TODO: Add sample data* |

### Alternative data sources for various scenarios

| Provider  | Scenario                                       | Data source                  | Authentication required | Request/Query Sample |
|:----------|:-----------------------------------------------|:-----------------------------|:------------------------|:---------------------|
| AWS       | Flat-rate based and quantity-dependent pricing | AWS Price List API           | N | [GET request](https://pricing.us-east-1.amazonaws.com/offers/v1.0/aws/AmazonS3/current/index.csv) |
| GCP       | Flat-rate based pricing                        | BigQuery Pricing Data Export | Y | Query:<pre>SELECT sku.id AS sku_id, sku.description AS sku_description, service.id AS service_id, service.description as service_description, pricing_unit, pricing_unit_description, account_currency_code, tier.*<br>FROM &grave;my-billing-admin-project.my_billing_dataset.cloud_pricing_export&grave; AS sku_pricing,  UNNEST (sku_pricing.list_price.tiered_rates) as tier <br>WHERE TIMESTAMP_TRUNC(_PARTITIONTIME, DAY) = TIMESTAMP("2023-08-24") AND sku.id = "0012-B7F2-DD14"<br>LIMIT 1000;</pre>Response:<pre>[{"sku_id":"0012-B7F2-DD14", "sku_description":"Spot Preemptible Compute optimized Ram running in Montreal", "service_id":"6F81-5844-456A", "service_description":"Compute Engine", "pricing_unit":"GIBIBYTE_HOUR", "pricing_unit_description":"gibibyte hour", "account_currency_code":"USD", "pricing_unit_quantity":"1.0", "start_usage_amount":"0.0", "usd_amount":"0.001537", "account_currency_amount":"0.001537"}]</pre>|
| GCP       | Quantity-dependent pricing                     | BigQuery Pricing Data Export | Y | Query:<pre>SELECT sku.id AS sku_id, sku.description AS sku_description, service.id AS service_id, service.description as service_description, pricing_unit, pricing_unit_description, account_currency_code, tier.*<br>FROM &grave;my-billing-admin-project.my_billing_dataset.cloud_pricing_export&grave; AS sku_pricing,  UNNEST (sku_pricing.list_price.tiered_rates) as tier <br>WHERE TIMESTAMP_TRUNC(_PARTITIONTIME, DAY) = TIMESTAMP("2023-08-24") AND sku.id = "3886-1DF3-046E"LIMIT 1000;</pre>Response:<pre>[{"sku_id":"3886-1DF3-046E", "sku_description":"Certificate", "service_id":"3C02-AF97-2288", "service_description":"AppViewX Inc AppViewX-CLM-v2", "pricing_unit":"DAY", "pricing_unit_description":"day", "account_currency_code":"USD", "pricing_unit_quantity":"1.0", "start_usage_amount":"0.0", "usd_amount":"0.0", "account_currency_amount":"0.0"},{"sku_id":"3886-1DF3-046E", "sku_description":"Certificate", "service_id":"3C02-AF97-2288", "service_description":"AppViewX Inc AppViewX-CLM-v2", "pricing_unit":"DAY", "pricing_unit_description":"day", "account_currency_code":"USD", "pricing_unit_quantity":"1.0", "start_usage_amount":"30001.0", "usd_amount":"0.09", "account_currency_amount":"0.09"}...]</pre>|
| GCP       | Flat-rate based pricing                        | GCP Cloud Billing API | Y | [GET request](https://cloudbilling.googleapis.com/v1beta/skus/0012-B7F2-DD14/price?currencyCode=USD) <br><br><pre>{"name":"skus/0012-B7F2-DD14/price", "currencyCode":"USD", "valueType":"rate", "rate":{"tiers":[{"startAmount":{"value":"0"},"listPrice":{"currencyCode":"USD", "nanos":1397000}}],"unitInfo":{"unit":"GiBy.h", "unitDescription":"gibibyte hour", "unitQuantity":{"value":"1"}},"aggregationInfo":{"level":"ACCOUNT", "interval":"MONTHLY"}}}</pre> |
| GCP       | Quantity-dependent pricing                     | GCP Cloud Billing API | Y | [GET request](https://cloudbilling.googleapis.com/v1beta/skus/0012-B7F2-DD14/price?currencyCode=USD) <br><br><pre>{"name":"skus/3886-1DF3-046E/price", "currencyCode":"USD", "valueType":"rate", "rate":{"tiers":[{"startAmount":{"value":"0"},"listPrice":{"currencyCode":"USD"}},{"startAmount":{"value":"300001"},"listPrice":{"currencyCode":"USD", "nanos":47000000}}...],"unitInfo":{"unit":"d", "unitDescription":"day", "unitQuantity":{"value":"1"}},"aggregationInfo":{"level":"LEVEL_ACCOUNT", "interval":"INTERVAL_MONTHLY"}}}</pre> |
| Microsoft | Flat-rate based pricing                        | Azure Retail Prices REST API | N | [GET request](https://prices.azure.com/api/retail/prices?api-version=2023-01-01-preview&currencyCode=%27EUR%27&meterRegion=%27primary%27&$filter=meterId%20eq%20%27b9e5e77c-a0b3-4a2c-9b8b-57fa54f31c52%27%20and%20location%20eq%20%27EU%20West%27) |
| Microsoft | Quantity-dependent pricing                     | Azure Retail Prices REST API | N | [GET request](https://prices.azure.com/api/retail/prices?api-version=2023-01-01-preview&currencyCode=%27USD%27&meterRegion=%27primary%27&$filter=meterId%20eq%20%279995d93a-7d35-4d3f-9c69-7a7fea447ef4%27%20%20and%20location%20eq%20%27EU%20West%27&$orderby=tierMinimumUnits%20asc) |
| OCI       | Flat-rate based pricing                        | OCI List Pricing REST API    | N | [GET request](https://apexapps.oracle.com/pls/apex/cetools/api/v1/products/?currencyCode=EUR&partNumber=B88513) |
| OCI       | Quantity-dependent pricing                     | OCI List Pricing REST API    | N | [GET request](https://apexapps.oracle.com/pls/apex/cetools/api/v1/products/?currencyCode=EUR&partNumber=B90617) |

## Discussion / Scratch space

* Quantity-driven pricing strategies might not be the most appropriate term
* See [Pricing Support – UCs and Data samples Spreadsheet](https://docs.google.com/spreadsheets/d/1AZ-vtkKeKwYc8rqhxP1zMTnAVAS-svmWQQmr8cpv-IM/edit#gid=117987709) for additional UC scenarios.
