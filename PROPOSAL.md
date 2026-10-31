# ShopStock

## Problem
Small shops in Phnom Penh keep extra stock in a storage room and track it in a notebook, so deliveries and goods taken to the shop are often not written down and nobody knows who moved what. The counts go wrong, and storage runs empty before anyone reorders.

## Users and roles
- **Storekeeper (Staff)**: searches products and sees what is left in storage; records deliveries in and goods sent to the shop; records damaged, expired or returned goods, which wait for the manager's approval; sees their own movements and their status, and a dashboard with their work today and what is running low.
- **Manager**: does everything a storekeeper does, plus manages products, categories and suppliers; approves or rejects write-offs; adjusts stock after counting a product; sees the reorder list, all movements, cost prices and the monthly report; adds, edits and deactivates storekeeper accounts.

## User stories
1. As a manager, I want to add a storekeeper account so that a new employee can use the system.
   Accepted when: the account is created with a name, username, phone number and temporary password; a username already in use shows "This username is already taken"; the storekeeper must set a new password at first login.
2. As a user, I want to log in so that I see the pages for my role.
   Accepted when: each role goes to its own dashboard (/dashboard, /manager/dashboard); a wrong username or password shows "Invalid username or password"; a deactivated account sees "This account is deactivated".
3. As a storekeeper, I want to search and filter products so that I can quickly see what is left in storage.
   Accepted when: the list shows 10 products per page; typing "coca" shows only products whose name or SKU contains "coca"; an empty result shows "No products match your search".
4. As a storekeeper, I want to record goods that arrive in storage so that the stock goes up.
   Accepted when: a whole quantity from 1 to 10,000 (PURCHASE or RETURN_FROM_SHOP) increases the quantity; 0, a negative number or a decimal shows "Quantity must be a whole number from 1 to 10,000"; a PURCHASE needs a supplier and may have an invoice number.
5. As a storekeeper, I want to record goods leaving storage so that the stock stays correct.
   Accepted when: TO_SHOP decreases the quantity at once; taking out more than is in stock shows "Not enough stock: only N left"; DAMAGED, EXPIRED or RETURN_TO_SUPPLIER needs a note and waits for the manager's approval.
6. As a storekeeper, I want to see my work and what is running low so that I can check my work at the end of a shift.
   Accepted when: my dashboard shows what I recorded today, my write-offs waiting or rejected, and the products running low, with no cost price or stock value; I see only my own movements, newest first, with their status; opening another storekeeper's movement shows the not-found page (404).
7. As a manager, I want to add, edit and archive products so that the catalogue matches what is in storage.
   Accepted when: a new product starts at quantity 0; a duplicate SKU shows "SKU already exists"; a product with movements can only be archived ("Archive it instead").
8. As a manager, I want to approve write-offs and correct a quantity after counting the shelf so that the system matches what is really in storage.
   Accepted when: approving a write-off changes the stock and rejecting needs a reason; counted 18 when the system says 20 saves an adjustment of −2 with a note; a count equal to the system shows "No difference to adjust".
9. As a manager, I want a reorder list and a monthly report so that I can reorder in time and see losses.
   Accepted when: products at or below their reorder level are grouped by supplier with a suggested order (3 left, target 20, order 17); the report shows stock in and out per category, the top 5 sent to the shop and losses; a month with no movements shows zeros.
10. As a manager, I want to manage staff accounts, categories and suppliers so that I control who uses the system and how products are grouped.
    Accepted when: I can deactivate a storekeeper but not myself ("You cannot deactivate your own account"); deleting a category or supplier that still has products shows "Move or delete its products first"; a storekeeper gets 403 on these actions.

## MVP scope
Must have: story 1, 2, 3, 4, 5, 6, 7, 8, 9, 10.
Nice to have: slow-moving products in the report, downloading the report as PDF or CSV, a product photo, a My profile page, and recording several products in one delivery.
Cut from the MVP: stock counts that storekeepers submit and the manager approves. They needed a sixth entity (StockCount), two more screens and an approval flow, which is too much for one person. The manager now adjusts stock directly after counting a product (story 8).

## Entities
| Entity | Main attributes | Relations |
|---|---|---|
| User | fullName, username, phone, passwordHash, role (STAFF, MANAGER), isActive, mustChangePassword, createdAt | has many StockMovements |
| Category | name, description | has many Products |
| Supplier | name, phone, email, address | has many Products; has many StockMovements (deliveries) |
| Product | sku, name, unit, costPrice, quantity, reorderLevel, targetLevel, isActive, imageUrl | belongs to a Category and a Supplier (optional); has many StockMovements |
| StockMovement | type (IN, OUT, ADJUST), reason, change, quantityAfter, unitCost, status (APPLIED, PENDING, REJECTED), invoiceNo, note, rejectReason, createdAt | belongs to a Product, a User (who recorded it) and a Supplier (PURCHASE only); reviewedBy a User |

## Stretch feature
Search + pagination.
What it does in this app: on the product list, storekeepers search by name or SKU (ignoring upper and lower case), filter by category, supplier and "low stock only", and see 10 products per page (at most 50); a page number below 1 returns 400, and an empty result shows "No products match your search".

## Repository
https://github.com/thawinner/ip1-e20230181

## Changes from the first proposal
Compared with the first version (`docs/proposal-old-version.pdf`). The idea, the two roles, the five entities, the tech stack and the stretch feature stay the same; the changes make ShopStock fit a shop's storage room better and keep the project small enough for one person.

| # | What changed | First version | Now | Why |
|---|---|---|---|---|
| 1 | Focus | The whole shop, including sales | Only the shop's storage room: goods come in from suppliers and go out to the shop | ShopStock does not sell, so selling did not belong in it |
| 2 | Reasons and prices | SALE, CUSTOMER_RETURN; sale price on each product ("Sale price cannot be lower than cost price") | TO_SHOP, RETURN_FROM_SHOP; no sale price; the report shows the top 5 products sent to the shop | Follows from change 1 |
| 3 | Accounts | Anyone registers with an email; the account waits until the manager activates it | The manager registers each storekeeper with a username, phone number and temporary password; the storekeeper sets their own password at first login | Storekeepers are employees, so the manager decides who gets an account; many do not use email |
| 4 | Write-offs | DAMAGED and EXPIRED change the stock at once | DAMAGED, EXPIRED and RETURN_TO_SUPPLIER need a note, and a storekeeper's waits for the manager's approval on a new Approvals page | Losses are where mistakes and theft happen, so the manager checks them |
| 5 | Deliveries | Any PURCHASE | A PURCHASE needs its supplier and can have an invoice number | So each delivery can be traced to its supplier |
| 6 | Products | A unit and a reorder level; every user sees the stock value | Storage unit (CASE, BOX, BAG, PACK or PIECE), reorder level and target level; each movement keeps the cost price of that day; staff do not see cost prices | Makes the reorder list and the stock value correct |
| 7 | Low stock | Low-stock alerts page | Reorder list grouped by supplier, with a suggested order (target level − quantity) | Tells the manager what to order and from whom |
| 8 | Monthly report | Stock in and out, top 5 sold, stock value | Adds losses with their value | Shows how much is lost each month |
| 9 | Dashboards | Manager dashboard only | Staff also open on a dashboard: their work today, write-offs waiting or rejected, products running low (story 6) | Staff see at a glance what needs attention |
| 10 | Adjustments | Manager adjusts stock after a count, with a note | Same, on an Adjust stock page opened from the product. A version where storekeepers submit counts for approval was tried in the mockup and cut | It needed a sixth entity, two more screens and an approval flow: too big for one person |
| 11 | Business rules | 9 | 19 (new: write-off approval, supplier on deliveries, target level, username, phone and password rules, the manager cannot deactivate their own account) | Each new feature has its rule and exact error message |
| 12 | Screens | 11 groups | 13 groups. Removed: /register, /manager/alerts. Added: /dashboard (staff), /password, /profile, /manager/approvals, /manager/reorder | Follows the changes above |
| 13 | Proposal format | Word document | This PROPOSAL.md, following the template in the project guideline | Required by the guideline |

### Stories renamed
| Story | First version | Now |
|---|---|---|
| 1 | Register (Staff) | Add a storekeeper account (Manager) |
| 4 | Record stock in | Record a delivery (stock in) |
| 5 | Record stock out | Send stock to the shop or write it off |
| 6 | See my movements | See my work (adds the staff dashboard) |
| 8 | Adjust stock after a count | Approve write-offs and adjust stock |
| 9 | Low-stock alerts and monthly report | Reorder list and monthly report |

Stories 2, 3, 7 and 10 keep their names; there are still 10 stories.

### Entity fields changed
| Entity | Added | Removed |
|---|---|---|
| User | username, phone, mustChangePassword, createdAt | email |
| Product | targetLevel, imageUrl | salePrice |
| StockMovement | unitCost, status, supplierId, invoiceNo, reviewedById, rejectReason | — |

Category and Supplier are unchanged.
