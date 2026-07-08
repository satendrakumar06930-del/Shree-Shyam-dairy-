1<!DOTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DairyFresh | Milk Delivery</title>

  <style>
    * {
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      margin: 0;
      background: #f4fbff;
      color: #17324d;
    }

    header {
      background: white;
      padding: 15px 7%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
      position: sticky;
      top: 0;
      z-index: 5;
    }

    .logo {
      font-size: 24px;
      font-weight: bold;
      color: #1375c9;
    }

    .logo span {
      color: #22a65a;
    }

    .cart-btn,
    .add-btn,
    .checkout-btn,
    .location-btn {
      border: none;
      border-radius: 8px;
      padding: 11px 15px;
      font-weight: bold;
      cursor: pointer;
    }

    .cart-btn,
    .add-btn {
      background: #1375c9;
      color: white;
    }

    .cart-btn:hover,
    .add-btn:hover {
      background: #075da6;
    }

    .hero {
      text-align: center;
      padding: 55px 20px;
      background: linear-gradient(135deg, #e7f5ff, #effff5);
    }

    .hero h1 {
      font-size: 38px;
      margin: 0 0 12px;
    }

    .hero p {
      color: #557089;
      margin: 0;
    }

    .products-title {
      text-align: center;
      margin: 40px 0 -20px;
      font-size: 28px;
    }

    .products {
      max-width: 1100px;
      margin: auto;
      padding: 45px 20px;
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 20px;
    }

    .product-card {
      background: white;
      padding: 24px;
      border-radius: 15px;
      text-align: center;
      box-shadow: 0 5px 18px rgba(0, 0, 0, 0.08);
    }

    .product-card h2 {
      margin: 8px 0;
      font-size: 22px;
    }

    .product-card p {
      color: #557089;
      min-height: 42px;
      line-height: 1.5;
    }

    .product-icon {
      font-size: 55px;
    }

    .price {
      color: #1375c9;
      font-weight: bold;
      font-size: 20px;
      margin: 15px 0;
    }

    .cart-panel {
      position: fixed;
      top: 0;
      right: -420px;
      width: 390px;
      max-width: 100%;
      height: 100vh;
      background: white;
      z-index: 20;
      padding: 22px;
      transition: right 0.3s;
      box-shadow: -5px 0 20px rgba(0, 0, 0, 0.15);
      overflow-y: auto;
    }

    .cart-panel.open {
      right: 0;
    }

    .cart-top {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #e7eef3;
      padding-bottom: 15px;
    }

    .close-btn,
    .close-payment {
      border: none;
      background: none;
      font-size: 30px;
      cursor: pointer;
    }

    .cart-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px 0;
      border-bottom: 1px solid #e7eef3;
    }

    .cart-item small,
    .empty,
    #locationStatus {
      color: #557089;
    }

    .quantity {
      display: flex;
      gap: 8px;
      align-items: center;
    }

    .quantity button {
      border: none;
      background: #e7f5ff;
      color: #1375c9;
      width: 28px;
      height: 28px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 18px;
    }

    .total {
      display: flex;
      justify-content: space-between;
      margin-top: 22px;
      font-size: 20px;
      font-weight: bold;
    }

    .checkout-btn {
      background: #22a65a;
      color: white;
      width: 100%;
      margin-top: 15px;
    }

    .checkout-btn:hover {
      background: #168043;
    }

    .modal {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0, 0, 0, 0.5);
      z-index: 50;
      align-items: center;
      justify-content: center;
      padding: 18px;
    }

    .modal.show {
      display: flex;
    }

    .payment-box {
      width: 100%;
      max-width: 450px;
      background: white;
      padding: 25px;
      border-radius: 15px;
      position: relative;
    }

    .payment-box h2 {
      margin-top: 0;
    }

    .close-payment {
      position: absolute;
      right: 15px;
      top: 10px;
    }

    .payment-box input,
    .payment-box textarea {
      width: 100%;
      padding: 12px;
      margin: 8px 0;
      border: 1px solid #cddce7;
      border-radius: 8px;
      outline: none;
    }

    .payment-box textarea {
      min-height: 80px;
      resize: vertical;
    }

    .location-btn {
      width: 100%;
      background: #e7f5ff;
      color: #1375c9;
      margin: 5px 0 10px;
    }

    .payment-option {
      display: block;
      padding: 12px 0;
      color: #17324d;
      font-size: 16px;
    }

    footer {
      background: #17324d;
      color: white;
      text-align: center;
      padding: 20px;
      margin-top: 20px;
    }

    @media (max-width: 800px) {
      .products {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    @media (max-width: 550px) {
      .products {
        grid-template-columns: 1fr;
      }

      .hero h1 {
        font-size: 30px;
      }

      .cart-panel {
        width: 100%;
        right: -100%;
      }
    }
  </style>
</head>

<body>

  <header>
    <div class="logo">Dairy<span>Fresh</span></div>

    <button class="cart-btn" onclick="toggleCart()">
      🛒 Cart (<span id="cartCount">0</span>)
    </button>
  </header>

  <section class="hero">
    <h1>Fresh Milk Delivered Daily 🥛</h1>
    <p>Pure dairy products for your family, delivered fresh.</p>
  </section>

  <h2 class="products-title">Our Milk Products</h2>

  <section class="products">
    <div class="product-card">
      <div class="product-icon">🐄🥛</div>
      <h2>Cow Milk</h2>
      <p>Fresh cow milk, light and healthy for daily use.</p>
      <div class="price">₹50 / litre</div>
      <button class="add-btn" onclick="addToCart('Cow Milk', 50)">Add to Cart</button>
    </div>

    <div class="product-card">
      <div class="product-icon">🐃🥛</div>
      <h2>Buffalo Milk</h2>
      <p>Thick and creamy buffalo milk with rich taste.</p>
      <div class="price">₹70 / litre</div>
      <button class="add-btn" onclick="addToCart('Buffalo Milk', 70)">Add to Cart</button>
    </div>

    <div class="product-card">
      <div class="product-icon">🥛✨</div>
      <h2>Mix Milk</h2>
      <p>Fresh cow and buffalo milk mix with balanced creaminess.</p>
      <div class="price">₹60 / litre</div>
      <button class="add-btn" onclick="addToCart('Mix Milk', 60)">Add to Cart</button>
    </div>

    <div class="product-card">
      <div class="product-icon">🥛</div>
      <h2>Full Cream Milk</h2>
      <p>Rich and creamy milk for tea, coffee and family use.</p>
      <div class="price">₹70 / litre</div>
      <button class="add-btn" onclick="addToCart('Full Cream Milk', 70)">Add to Cart</button>
    </div>

    <div class="product-card">
      <div class="product-icon">🧃</div>
      <h2>Toned Milk</h2>
      <p>Fresh and light milk for everyday drinking.</p>
      <div class="price">₹50 / litre</div>
      <button class="add-btn" onclick="addToCart('Toned Milk', 50)">Add to Cart</button>
    </div>

    <div class="product-card">
      <div class="product-icon">🧈</div>
      <h2>Fresh Curd</h2>
      <p>Thick and tasty curd for meals and snacks.</p>
      <div class="price">₹45 / 500g</div>
      <button class="add-btn" onclick="addToCart('Fresh Curd', 45)">Add to Cart</button>
    </div>
  </section>

  <aside class="cart-panel" id="cartPanel">
    <div class="cart-top">
      <h2>Your Cart</h2>
      <button class="close-btn" onclick="toggleCart()">×</button>
    </div>

    <div id="cartItems">
      <p class="empty">Your cart is empty.</p>
    </div>

    <div class="total">
      <span>Total</span>
      <span>₹<span id="totalPrice">0</span></span>
    </div>

    <button class="checkout-btn" onclick="checkout()">Place Order</button>
  </aside>

  <div class="modal" id="checkoutModal">
    <div class="payment-box">
      <button class="close-payment" onclick="closePayment()">×</button>

      <h2>Delivery Details</h2>
      <p>Total Amount: ₹<span id="paymentTotal">0</span></p>

      <form onsubmit="placeOrder(event)">
        <input type="text" id="customerName" placeholder="Your Name" required>
        <input type="tel" id="customerPhone" placeholder="Phone Number" required>
        <textarea id="customerAddress" placeholder="Full Delivery Address" required></textarea>

        <button type="button" class="location-btn" onclick="getLocation()">
          📍 Use My Current Location
        </button>

        <p id="locationStatus"></p>

        <div class="payment-option">
          💵 Payment Method: <strong>Cash on Delivery (COD)</strong>
        </div>

        <button class="checkout-btn" type="submit">Confirm Order on WhatsApp</button>
      </form>
    </div>
  </div>

  <footer>
    <p>© 2026 DairyFresh | Fresh milk every day</p>
  </footer>

  <script>
    let cart = [];

    function addToCart(name, price) {
      const found = cart.find(function(item) {
        return item.name === name;
      });

      if (found) {
        found.quantity += 1;
      } else {
        cart.push({
          name: name,
          price: price,
          quantity: 1
        });
      }

      updateCart();
    }

    function updateCart() {
      const cartItems = document.getElementById("cartItems");
      const cartCount = document.getElementById("cartCount");
      const totalPrice = document.getElementById("totalPrice");

      let total = 0;
      let count = 0;

      if (cart.length === 0) {
        cartItems.innerHTML = '<p class="empty">Your cart is empty.</p>';
      } else {
        cartItems.innerHTML = "";

        cart.forEach(function(item, index) {
          total += item.price * item.quantity;
          count += item.quantity;

          cartItems.innerHTML +=
            '<div class="cart-item">' +
              '<div>' +
                '<strong>' + item.name + '</strong><br>' +
                '<small>₹' + item.price + ' each</small>' +
              '</div>' +
              '<div class="quantity">' +
                '<button onclick="changeQuantity(' + index + ', -1)">−</button>' +
                '<span>' + item.quantity + '</span>' +
                '<button onclick="changeQuantity(' + index + ', 1)">+</button>' +
              '</div>' +
            '</div>';
        });
      }

      cartCount.textContent = count;
      totalPrice.textContent = total;
    }

    function changeQuantity(index, change) {
      cart[index].quantity += change;

      if (cart[index].quantity <= 0) {
        cart.splice(index, 1);
      }

      updateCart();
    }

    function toggleCart() {
      document.getElementById("cartPanel").classList.toggle("open");
    }

    function checkout() {
      if (cart.length === 0) {
        alert("Please add milk products first.");
        return;
      }

      document.getElementById("paymentTotal").textContent =
        document.getElementById("totalPrice").textContent;

      document.getElementById("checkoutModal").classList.add("show");
    }

    function closePayment() {
      document.getElementById("checkoutModal").classList.remove("show");
    }

    function getLocation() {
      const status = document.getElementById("locationStatus");

      if (!navigator.geolocation) {
        status.textContent = "Location is not supported on this device.";
        return;
      }

      status.textContent = "Getting your location...";

      navigator.geolocation.getCurrentPosition(
        function(position) {
          const latitude = position.coords.latitude;
          const longitude = position.coords.longitude;

          document.getElementById("customerAddress").value =
            "Current location: Latitude " + latitude.toFixed(6) +
            ", Longitude " + longitude.toFixed(6);

          status.textContent =
            "Location added. Also write your house number and area.";
        },
        function() {
          status.textContent =
            "Location permission was denied. Enter address manually.";
        }
      );
    }

    function placeOrder(event) {
      event.preventDefault();

      const name = document.getElementById("customerName").value;
      const phone = document.getElementById("customerPhone").value;
      const address = document.getElementById("customerAddress").value;
      const payment = "Cash on Delivery (COD)";
      const total = document.getElementById("totalPrice").textContent;
      const ownerNumber = "919758180248";

      let productList = "";

      cart.forEach(function(item) {
        productList +=
          "- " + item.name +
          " x " + item.quantity +
          " = ₹" + (item.price * item.quantity) +
          "\n";
      });

      const message =
        "🥛 NEW MILK ORDER\n\n" +
        "Products:\n" + productList + "\n" +
        "Customer Name: " + name + "\n" +
        "Phone: " + phone + "\n" +
        "Address: " + address + "\n" +
        "Payment: " + payment + "\n" +
        "Total: ₹" + total;

      window.open(
        "https://wa.me/" + ownerNumber + "?text=" + encodeURIComponent(message),
        "_blank"
      );

      alert("WhatsApp is opening. Tap Send to place your order.");

      cart = [];
      updateCart();
      closePayment();
      document.getElementById("cartPanel").classList.remove("open");
      event.target.reset();
    }
  </script>

</body>
</html>
