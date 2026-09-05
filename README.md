# Bulding materials

IMPLEMENTATION SEQUENCE

Build the application in the following order. Do not skip ahead or implement all modules simultaneously.

Phase 1 — Application Foundation

1. Create the React + TypeScript + Vite application.

2. Configure Tailwind CSS and shadcn/ui or an equivalent component system.

3. Set up React Router.

4. Create the base folder structure:

   - "components"

   - "layouts"

   - "pages"

   - "features"

   - "services"

   - "types"

   - "hooks"

   - "utils"

5. Create the global design system:

   - colors

   - typography

   - spacing

   - buttons

   - inputs

   - tables

   - badges

   - dialogs

   - cards

   - toast notifications

6. Make the application responsive, desktop-first, and accessible.

Phase 2 — Authentication

1. Create "/shopkeeper/login".

2. Build the Shopkeeper Login screen.

3. Add mobile number and password fields.

4. Add validation.

5. Add login loading/error states.

6. Create a simple mock authentication service initially.

7. Protect all "/shopkeeper/*" routes.

8. Add logout functionality.

9. Do not add Google, Facebook, Apple, OTP, or social login.

Phase 3 — Shopkeeper Layout

1. Create the reusable "ShopkeeperLayout".

2. Add the sidebar navigation.

3. Add the top header.

4. Add shop name and shopkeeper profile area.

5. Add responsive sidebar behavior.

6. Configure navigation routes:

   

   - Dashboard

   - Products

   - Categories

   - Brands

   - Stock

   - Stock History

   - Orders

   - Sales Reports

   - Shop Settings

   - Logout

7. Create placeholder pages for modules that are not implemented yet.

8. Do not build those future modules in this phase.

Phase 4 — Products Data Model and Services

Create the Products module before building the detailed UI.

Create the following TypeScript models:

Product

- id

- name

- categoryId

- brandId

- description

- imageUrl

- sellingUnit

- sellingPrice

- minimumOrderQuantity

- visibilityStatus

- createdAt

- updatedAt

Create the inventory model:

Inventory

- id

- productId

- currentStock

- lowStockThreshold

- updatedAt

Create order-item history support:

OrderItem

- productId

- productName

- quantity

- unit

- unitPriceAtOrder

- subtotal

Create a product service abstraction:

getProducts()

getProduct(id)

createProduct(product)

updateProduct(id, product)

setProductVisibility(id, status)

Initially use mock/in-memory/local data, but keep the service layer separated from the UI so it can later be replaced with REST APIs.

Phase 5 — Products List

Implement "/shopkeeper/products".

Build:

1. Page header

   - Products

   - Add Product button

2. Search

   - Product name

   - Brand

   - Category

3. Filters

   - Category

   - Brand

   - Status

4. Products table with:

   - Product

   - Category

   - Brand

   - Selling Unit

   - Price

   - Stock

   - Status

   - Actions

5. Actions:

   - Visible product → Edit, Hide

   - Hidden product → Edit, Show

6. Add pagination-ready structure.

7. Add:

   - loading state

   - empty state

   - search-empty state

   - error state

   - success toast

Use realistic sample data such as:

Ramco PPC Cement | Cement | Ramco | Bag | ₹420/Bag | 120 Bags | Visible

Ultratech OPC 53 | Cement | Ultratech | Bag | ₹450/Bag | 85 Bags | Visible

Tata 12mm TMT | Steel | Tata | Kg | ₹72/Kg | 850 Kg | Visible

Red Clay Brick | Bricks | Local | Piece | ₹9/Piece | 5,000 Pieces | Hidden

River Sand | Sand | Local | Load | ₹5,500/Load | 8 Loads | Visible

Phase 6 — Add Product

Implement "/shopkeeper/products/new".

Use a four-step workflow.

Step 1 — Basic Information

Fields:

- Product Name

- Category

- Brand

- Description

- Product Image

Add validation.

Step 2 — Selling Information

Fields:

- Selling Unit

- Selling Price

- Minimum Order Quantity

Example:

Selling Unit: Bag

Selling Price: ₹420

Minimum Order Quantity: 1

Step 3 — Inventory

Fields:

- Track Inventory

- Current Stock

- Low Stock Threshold

Example:

Track Inventory: Yes

Current Stock: 120

Low Stock Threshold: 20

Step 4 — Visibility & Review

Fields:

- Visible / Hidden

Show a complete review summary before submission.

On successful creation:

1. Save the product through the product service.

2. Show success feedback.

3. Navigate to Product Details or Products List.

4. Ensure the newly created product appears correctly.

Phase 7 — Product Details

Implement:

"/shopkeeper/products/:id"

Display:

- Product image

- Product name

- Category

- Brand

- Description

- Selling unit

- Current selling price

- Minimum order quantity

- Current stock

- Low stock threshold

- Visibility status

- Created date

- Last updated date

Actions:

- Edit Product

- Hide Product / Show Product

Do not provide Delete as the primary action.

Phase 8 — Edit Product

Implement:

"/shopkeeper/products/:id/edit"

Allow editing:

- Product Name

- Category

- Brand

- Description

- Product Image

- Selling Unit

- Selling Price

- Minimum Order Quantity

- Visibility

Display current inventory information, but do not implement stock adjustment here.

Stock adjustment belongs to the future Inventory module.

Important pricing rule:

If a product currently costs ₹420/Bag and the shopkeeper changes it to ₹435/Bag:

- Existing historical orders must continue showing their original price.

- New orders must use ₹435/Bag.

- Never overwrite historical order-item prices.

Example:

Old Order #1024

10 Bags × ₹420 = ₹4,200

New Order

10 Bags × ₹435 = ₹4,350

Phase 9 — Hide / Show Product

Implement confirmation dialogs.

Hide Product

Show:

- Product name

- Current status

- Explanation that hidden products will no longer appear to customers.

After confirmation:

visibilityStatus = HIDDEN

The product remains in the database and retains its inventory/history.

Show Product

After confirmation:

visibilityStatus = VISIBLE

The product becomes available to customers again.

Phase 10 — Customer Visibility Rule

Create the business rule now even though the complete customer module will be implemented later:

Only products with visibilityStatus = VISIBLE

are allowed to appear in customer product browsing.

Hidden products must never appear in customer-facing product lists.

Phase 11 — Quality Pass

After the Products module is implemented, perform a complete pass for:

- TypeScript errors

- broken routes

- form validation

- loading states

- empty states

- error handling

- toast messages

- confirmation dialogs

- responsive layouts

- keyboard navigation

- accessible labels

- button states

- search behavior

- filtering behavior

- price formatting

- INR formatting

- hidden/visible state consistency

- mock data consistency

Phase 12 — Final Products Module Acceptance Test

Verify this complete flow:

Login

  ↓

Shopkeeper Dashboard

  ↓

Products

  ↓

Search / Filter

  ↓

Add Product

  ↓

Basic Information

  ↓

Selling Information

  ↓

Inventory

  ↓

Visibility & Review

  ↓

Create Product

  ↓

Product Created

  ↓

Product Details

  ↓

Edit Product

  ↓

Change Price

  ↓

Save

  ↓

Products List

  ↓

Hide Product

  ↓

Confirm

  ↓

Product becomes Hidden

  ↓

Show Product

  ↓

Confirm

  ↓

Product becomes Visible

IMPORTANT IMPLEMENTATION RULE

Build and stabilize each phase before moving to the next phase.

Do not generate Dashboard, Categories, Brands, Inventory, Orders, Sales Reports, or Shop Settings functionality beyond their required placeholder routes until the Products module is complete.

The immediate goal is:

Authentication → Shopkeeper Layout → Products List → Add Product → Product Details → Edit Product → Hide/Show Product → Quality Pass

Only after this flow works end-to-end should additional shopkeeper modules be implemented.

This project was built with [Lovable](https://lovable.dev).

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/a62c3ccc-50b3-48fd-a8a0-4b14e3be07b2).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
