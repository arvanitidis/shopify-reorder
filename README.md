# shopify-reorder
Display recent orders for customer and give option to reorder entire order

Placed this in customer account template to display list of past orders with option to reorder.

```
<table class="full">
  <thead>
    <tr>
      <th>{{ 'customer.orders.order_number' | t }}</th>
      <th>{{ 'customer.orders.date' | t }}</th>
      <th>{{ 'customer.orders.payment_status' | t }}</th>
      <th>{{ 'customer.orders.fulfillment_status' | t }}</th>
      <th>{{ 'customer.orders.total' | t }}</th>
      <th>&nbsp;</th>
    </tr>
  </thead>
  <tbody>
    {% for order in customer.orders %}
      <tr>
        <td>{{ order.name | link_to: order.customer_url }}</td>
        <td>{{ order.created_at | date: format: 'month_day_year' }}</td>
        <td>{{ order.financial_status_label }}</td>
        <td>{{ order.fulfillment_status_label }}</td>
        <td>{{ order.total_price | money }}</td>
        <td><a href="/cart/{% for line_item in order.line_items %}{{ line_item.variant_id }}:{{ line_item.quantity }}{% unless forloop.last %},{% endunless %}{% endfor %}">Reorder This</a></td>
      </tr>
    {% endfor %}
  </tbody>
</table>
```
