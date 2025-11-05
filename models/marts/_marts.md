{% docs dim_customers_desc %}

# Customer Dimension

This table contains customer data with additional metrics like:
- First and last order dates
- Number of orders
- Total lifetime value

It serves as the single source of truth for customer information in the Jaffle Shop data warehouse.

{% enddocs %}

{% docs fct_orders_desc %}

# Orders Fact Table

This table contains order transactions with:
- Order details
- Customer references
- Order status
- Order amounts

This is the primary fact table for analyzing order transactions.

{% enddocs %}