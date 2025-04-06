
# 📘 ER Diagram: Bookstore Order Management System

This ER diagram represents the **database structure** of a **bookstore** or **online book ordering system**. It captures key entities, their attributes, and relationships involved in managing books, customers, orders, authors, and shipping.

---

## 🔑 Main Entities & Relationships

### 🧍‍♂️ Customer
- `customer_id` (PK)
- `first_name`, `last_name`, `email`
- A customer can have **multiple addresses** via `customer_address`.
- A customer can place **multiple orders** via `cust_order`.

---

### 📦 Cust_Order (Customer Order)
- `order_id` (PK)
- `order_date`, `customer_id` (FK)
- `shipping_method_id` (FK), `dest_address_id` (FK)
- Each order is linked to:
  - One customer
  - One shipping method
  - One delivery address
  - One or more books (via `order_line`)

---

### 🛒 Order_Line
- `line_id` (PK)
- `order_id` (FK), `book_id` (FK)
- `price`
- Represents **line items** in an order (multiple books per order).

---

### 📚 Book
- `book_id` (PK)
- `title`, `isbn13`, `language_id`, `num_pages`, `publication_date`, `publisher_id` (FK)
- Linked to:
  - A **publisher**
  - One or more **authors** (via `book_author`)
  - A **language**

---

### ✍️ Author
- `author_id` (PK)
- `author_name`
- Many-to-Many with `book` using junction table `book_author`.

---

### 🖋️ Publisher
- `publisher_id` (PK)
- `publisher_name`
- One publisher can publish many books.

---

### 🌍 Book_Language
- `language_id` (PK)
- `language_code`, `language_name`

---

### 🚚 Shipping_Method
- `method_id` (PK)
- `method_name`, `cost`
- Represents shipping options available for an order.

---

### 🧾 Order_Status
- `status_id` (PK)
- `status_value` (e.g., "Pending", "Shipped", "Delivered")

---

### 🔁 Order_History
- `history_id` (PK)
- `order_id` (FK), `status_id` (FK), `status_date`
- Tracks the **status changes** over time for each order.

---

### 📍 Address
- `address_id` (PK)
- `street_number`, `street_name`, `city`, `country_id` (FK)
- Used for both billing and delivery.

---

### 🌐 Country
- `country_id` (PK)
- `country_name`

---

### 🏠 Customer_Address
- Links `customer_id` and `address_id`
- Includes `status_id` (FK) to define address type (e.g., shipping, billing)

---

### ✅ Address_Status
- `status_id` (PK)
- `address_status` (e.g., "Billing", "Shipping")

---

## 🔗 Relationships Summary

| From | To | Type |
|------|----|------|
| Customer | Cust_Order | One-to-Many |
| Cust_Order | Order_Line | One-to-Many |
| Book | Order_Line | One-to-Many |
| Book | Publisher | Many-to-One |
| Book | Author | Many-to-Many |
| Book | Book_Language | Many-to-One |
| Cust_Order | Shipping_Method | Many-to-One |
| Cust_Order | Address | Many-to-One (Delivery Address) |
| Address | Country | Many-to-One |
| Customer | Address | Many-to-Many (via `customer_address`) |
| Order_History | Order_Status | Many-to-One |
| Cust_Order | Order_History | One-to-Many |

---

## 🧩 Use Case
This database can power an online bookstore or publishing service backend by tracking:
- Customer info & order history
- Book catalog with author/publisher details
- Shipping logistics
- Order status lifecycle
