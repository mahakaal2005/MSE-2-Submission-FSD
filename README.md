# KIET_FSD_DebugChallenge

Bug Sheet — ShopEasy Debugging Assignment
Instructions: Find and fix all 9 bugs spread across 4 files. The app compiles and runs without errors — all bugs are logical/behavioral.

Bug 1 — App.js | Easy
Symptom: Price range filters exclude products at the exact boundary price (e.g. "Under ₹500" won't show the ₹499 product; "₹500–₹1,000" won't show the ₹500 or ₹1,000 products).
Solution -> In App.js line 22
prev ->"const matchPrice = p.price > priceRange.min && p.price < priceRange.max;"

new ->"const matchPrice = p.price >= priceRange.min && p.price <= priceRange.max;"



Bug 2 — App.js | Hard
Symptom: Clicking any Category button (Electronics, Footwear, etc.) has no effect — the product grid never changes.
Solution -> In App.js line 35

prev ->"[searchQuery, priceRange, sortBy] "

new ->"[searchQuery, priceRange, sortBy ,category]"


Bug 3 — App.js | Easy
Symptom: Clicking the 🗑️ delete button in the cart removes all other items and keeps only the one you tried to delete.
Solution -> In App.js line 47

prev ->"setCartItems(prev => prev.filter(i => i.id === id));"

new ->"setCartItems(prev => prev.filter(i => i.id !== id));"


Bug 4 — App.js | Medium
Symptom: The cart badge on the header button always shows nothing (or 0) even after adding multiple items.
Solution -> In App.js line 55

prev ->"const cartCount = cartItems.reduce((sum, i) => sum + i.count, 0);"

new ->"const cartCount = cartItems.reduce((sum, i) => sum + i.qty, 0);"


Bug 5 — App.js | Hard
Symptom: The "+ Add to Cart" button never turns green and never says "✓ Added", even after a product is in the cart.
Solution -> In App.js line 56

prev ->"const cartItemIds = new Set(cartItems.map(i => i.productId));"

new ->"const cartItemIds = new Set(cartItems.map(i => i.id));"


Bug 6 — Cart.jsx | Medium
Symptom: The cart total always shows ₹0, no matter how many items or quantities are added.
Solution -> In Cart.jsx line 4

prev ->"const total = items.reduce((sum, item) => sum + item.price * item.count, 0);"

new ->"const total = items.reduce((sum, item) => sum + item.price * item.qty, 0);"


Bug 7 — Cart.jsx | Medium
Symptom: The − (decrease) button in the cart is never disabled, allowing quantity to drop to 0 (and below), breaking the total.
Solution -> In Cart.jsx line 33

prev ->"disabled={item.qty <= 0}"

new ->"disabled={item.qty <= 1}"


Bug 8 — Filters.jsx | Easy
Symptom: The sort order is inverted — selecting "Price: Low to High" sorts highest-priced items first, and vice versa.
Solution -> In Filters.jsx line 59

prev ->"<option value="price-desc">Price: Low to High</option>
        <option value="price-asc">Price: High to Low</option>"

new ->"<option value="price-asc">Price: Low to High</option>
        <option value="price-desc">Price: High to Low</option>"


Bug 9 — ProductCard.jsx | Easy
Symptom: A product rated 4.5 shows only 4 filled stars instead of 5. All half-star ratings are rounded down.
Solution -> In ProductCard.jsx line 7

prev ->"<span key={star} className={star <= Math.floor(rating) ? 'star filled' : 'star'}>★</span>"

new ->"<span key={star} className={star <= Math.round(rating) ? 'star filled' : 'star'}>★</span>"
