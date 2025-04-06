
# 🚀 The SQL Project That Launched My Data Science Journey

Every Data Scientist needs to get their hands dirty with data—and for me, it all started with this ER diagram.

When I first looked at it, I didn’t just see boxes and lines. I saw structure. I saw flow. I saw *potential*. That was the moment I realized—if I wanted to step into the world of Data Science, I had to go deep into how data actually works behind the scenes. And what better way to do that than by building my own SQL project from scratch?

---

## 📊 Breaking Down the Data Model

This database was originally built to manage a bookstore’s order system, but to me, it became so much more than that.

- 🣍️ `customer` holds all the basic info about users.
- 💾 `cust_order` logs every order along with dates, shipping, and address.
- 📚 `book` is connected with `author`, `publisher`, and even language—perfect for building a rich dataset.
- 🔁 `order_history` lets me trace how each order changes over time.

Each table told a part of the story. And writing SQL queries was like asking the data to reveal its secrets.

---

## 🔍 My First Real Data Science Moves

As I played with the data, something clicked—I was no longer just querying; I was analyzing.

- ✅ Aggregation: Figured out top-selling books, best months for sales, and patterns in customer behavior.
- ✅ Customer Trends: Found repeat buyers, their favorite genres, and how often they placed orders.

This wasn’t just SQL anymore. This was the beginning of my journey into real analytics—and it felt amazing.

---

## 🎯 What I Took Away from This

- 🧠 Understanding how databases work is the *foundation* of Data Science.
- 🛠️ SQL is more than just syntax—it’s a powerful tool to *ask questions and get answers*.
- 📌 ER diagrams? They’re not just technical docs—they’re maps for discovering stories in your data.

---

If you’re starting out in Data Science, I can’t recommend this enough: **Build something**. Explore. Write queries. Make mistakes. Learn.

This project wasn’t just about data—it was about discovering my path.

---

This ER diagram represents the **database structure** of a **bookstore** or **online book ordering system**. It captures key entities, their attributes, and relationships involved in managing books, customers, orders, authors, and shipping.

---
# 📘 ER Diagram: Bookstore Order Management System

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
