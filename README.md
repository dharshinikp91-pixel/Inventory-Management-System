# Inventory-Management-System
This is to manage inventory within an organisation
Table Categories {
  category_id int [pk, increment]
  category_name varchar
  description text
  is_active boolean
  created_at datetime
}

Table Brands {
  brand_id int [pk, increment]
  brand_name varchar
  is_active boolean
  created_at datetime
}

Table UOM {
  uom_id int [pk, increment]
  uom_name varchar
}

Table Vendors {
  vendor_id int [pk, increment]
  vendor_code varchar [unique]
  vendor_name varchar
  contact_person varchar
  phone varchar
  email varchar
  address text
  gst_number varchar
  payment_terms varchar
  is_active boolean
  created_at datetime
}

Table Customers {
  customer_id int [pk, increment]
  customer_code varchar [unique]
  customer_name varchar
  contact_person varchar
  phone varchar
  email varchar
  address text
  gst_number varchar
  credit_limit decimal
  payment_terms varchar
  is_active boolean
  created_at datetime
}

Table Employees {
  employee_id int [pk, increment]
  employee_code varchar [unique]
  employee_name varchar
  designation varchar
  phone varchar
  email varchar
  is_active boolean
  created_at datetime
}

Table Products {
  product_id int [pk, increment]
  product_code varchar [unique]
  product_name varchar

  brand_id int
  category_id int
  uom_id int

  purchase_price decimal
  selling_price decimal

  reorder_level int

  hsn_code varchar
  gst_percentage decimal

  is_active boolean
  created_at datetime
}

Table Purchase_Order {
  po_id int [pk, increment]
  po_number varchar [unique]

  vendor_id int

  po_date date
  expected_delivery_date date

  status varchar

  total_amount decimal

  created_by int
  created_at datetime
}

Table Purchase_Order_Line {
  po_line_id int [pk, increment]

  po_id int
  product_id int

  quantity_ordered int
  quantity_received int

  unit_price decimal
  line_total decimal
}

Table Inventory {
  inventory_id int [pk, increment]

  product_id int

  current_stock int

  last_updated datetime
}

Table Sales_Order {
  so_id int [pk, increment]
  so_number varchar [unique]

  customer_id int

  order_date date
  required_date date

  status varchar

  total_amount decimal

  created_by int
  created_at datetime
}

Table Sales_Order_Line {
  so_line_id int [pk, increment]

  so_id int
  product_id int

  quantity_ordered int
  quantity_shipped int

  unit_price decimal
  line_total decimal
}

Ref: Products.category_id > Categories.category_id
Ref: Products.brand_id > Brands.brand_id
Ref: Products.uom_id > UOM.uom_id

Ref: Purchase_Order.vendor_id > Vendors.vendor_id
Ref: Purchase_Order.created_by > Employees.employee_id

Ref: Purchase_Order_Line.po_id > Purchase_Order.po_id
Ref: Purchase_Order_Line.product_id > Products.product_id

Ref: Inventory.product_id > Products.product_id

Ref: Sales_Order.customer_id > Customers.customer_id
Ref: Sales_Order.created_by > Employees.employee_id

Ref: Sales_Order_Line.so_id > Sales_Order.so_id
Ref: Sales_Order_Line.product_id > Products.product_id
