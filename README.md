# Sale Order Multiple Delivery

## Overview
**Sale Order Multiple Delivery** is an Odoo custom module that alters the default behavior of delivery order generation from Sale Orders. By default, Odoo groups stock moves (products) into a single delivery order based on the destination and picking type. This module modifies this process to create **multiple delivery orders** based on the **Product Category**.

When a Sale Order is confirmed, this module groups the stock moves by the `categ_id` (Product Category) of each product and creates a separate Delivery Order (`stock.picking`) for each distinct product category.

## Features
* **Category-based Delivery Splitting**: Automatically splits deliveries so that products belonging to different product categories are placed into distinct delivery orders.
* **Seamless Integration**: Hooks directly into the `_assign_picking` method of `stock.move`, ensuring the split happens naturally during the standard Odoo picking assignment process.

## Technical Details
* **Depends on**: `sale`, `stock`
* **Odoo Version**: 16.0
* **Core Logic**: Overrides the `_assign_picking` method in the `stock.move` model. It iterates over the generated stock moves, groups them into a dictionary by `move.product_id.categ_id`, and then creates a new `stock.picking` for each category group.

## Installation
1. Place the `SO_multiple_delivery` folder into your Odoo `addons` path.
2. Update the app list in Odoo.
3. Search for "SO Multiple Delivery" in the Apps menu.
4. Click **Install**.

## Usage
1. Create a new Sale Order.
2. Add multiple products that belong to **different Product Categories**.
3. Confirm the Sale Order.
4. Check the generated Deliveries (Smart button on the top right). You will notice that Odoo has generated multiple Delivery Orders, separated by the product categories of the items ordered.
