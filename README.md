# Jaffle Shop dbt Project

This repository contains a dbt project that transforms raw Jaffle Shop and Stripe payment data into a usable data model for analytics.

## Project Overview

This project demonstrates dbt fundamentals by building a small but realistic analytics engineering workflow. It transforms raw data from a fictional shop called "Jaffle Shop" (which sells sandwiches) along with payment data from Stripe into a clean, tested, and documented data model.

## Data Model

The project follows a typical staging + mart pattern:

### Sources
- **jaffle_shop**: Customer and order data
- **stripe**: Payment data

### Staging Models
- **stg_jaffle_shop__customers**: Cleaned customer data
- **stg_jaffle_shop__orders**: Cleaned order data
- **stg_stripe__payment**: Cleaned payment data with amounts converted from cents to dollars

### Mart Models
- **dim_customers**: Customer dimension with order metrics and lifetime value
- **fct_orders**: Order fact table with payment amounts

## Project Structure

```
├── models
│   ├── marts
│   │   ├── _marts.md                 # Documentation for mart models
│   │   ├── _marts.yml                # Configuration for mart models
│   │   ├── finance
│   │   │   └── fct_orders.sql        # Order fact table
│   │   └── marketing
│   │       └── dim_customers.sql     # Customer dimension table
│   └── staging
│       ├── jaffle_shop
│       │   ├── _jaffle_shop.md       # Documentation for jaffle_shop models
│       │   ├── _stg_jaffle_shop.yml  # Configuration for jaffle_shop models
│       │   ├── src_jaffle_shop.yml   # Source configuration for jaffle_shop
│       │   ├── stg_jaffle_shop__customers.sql
│       │   └── stg_jaffle_shop__orders.sql
│       └── stripe
│           ├── _src_stripe.yml       # Source configuration for stripe
│           ├── _stg_stripe.yml       # Configuration for stripe models
│           ├── _stripe.md            # Documentation for stripe models
│           └── stg_stripe__payment.sql
├── tests
│   └── assert_positive_value_for_total_amount.sql  # Custom test for payment amounts
└── dbt_project.yml                   # Main project configuration
```

## Key Features Implemented

1. **Modular Structure**
   - Separated staging and mart models
   - Organized by business domain (finance, marketing)

2. **Sources**
   - Configured sources for raw data
   - Added source freshness checks for payment data

3. **Transformations**
   - Basic column renaming and cleanup in staging models
   - Joined data across sources in mart models
   - Calculated metrics like lifetime value

4. **Testing**
   - Generic tests (unique, not_null, relationships, accepted_values)
   - Custom test for positive payment amounts

5. **Documentation**
   - Model and column descriptions
   - Doc blocks for reusable documentation
   - Markdown formatting for detailed explanations

6. **Materializations**
   - Configured staging models as views
   - Configured mart models as tables

## Getting Started

### Prerequisites
- dbt installed
- Access to a data warehouse with the raw data loaded

### Setup
1. Clone this repository
2. Update the profile in `dbt_project.yml` if needed
3. Run `dbt deps` to install dependencies
4. Run `dbt run` to build the models
5. Run `dbt test` to test the models
6. Run `dbt docs generate` and `dbt docs serve` to view documentation

## Usage Examples

### Building specific models
```bash
# Build all models
dbt run

# Build only staging models
dbt run --models staging

# Build only mart models
dbt run --models marts

# Build a specific model
dbt run --models dim_customers
```

### Testing
```bash
# Run all tests
dbt test

# Test specific models
dbt test --models stg_jaffle_shop__customers
```

### Documentation
```bash
# Generate documentation
dbt docs generate

# Serve documentation locally
dbt docs serve
```

## Notes for BigQuery Users

This project is configured for BigQuery. The database name is set to `dbt-tutorial` instead of `raw` in the source configurations.

## Additional Resources

- [dbt Documentation](https://docs.getdbt.com/)
- [dbt Discourse](https://discourse.getdbt.com/)
- [dbt Slack](https://community.getdbt.com/)