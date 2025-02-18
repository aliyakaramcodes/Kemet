<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kemet - Natural Skincare</title>
    <script type="text/javascript" src="https://cdn.emailjs.com/dist/email.min.js"></script>
    <style>
        body {
            font-family: "Arial", sans-serif;
            background-color: #2F3B2E;
            color: #E0C097;
            text-align: center;
            padding: 20px;
        }
        header {
            background-color: #7B4F2B;
            padding: 20px;
            font-size: 24px;
            border-bottom: 3px solid #E0C097;
        }
        .logo {
            max-width: 150px;
            display: block;
            margin: 0 auto 10px;
        }
        .product {
            border: 2px solid #E0C097;
            padding: 15px;
            margin: 20px;
            background-color: #4F3A2D;
            border-radius: 10px;
        }
        button {
            background-color: #E0C097;
            color: #2F3B2E;
            padding: 10px;
            border: none;
            cursor: pointer;
            font-size: 18px;
        }
        #cart {
            background-color: #7B4F2B;
            padding: 15px;
            margin: 20px auto;
            width: 50%;
            border-radius: 10px;
            text-align: left;
        }
    </style>
</head>
<body>
    <header>
        <img src="IMG_4743.png" alt="Kemet Logo" class="logo">
        <h1>Kemet Natural Skincare</h1>
    </header>
    
    <div class="product" id="dermaHeal">
        <h2>DermaHeal</h2>
        <p>A natural skincare remedy to reduce burn scars, even out skin tone, and promote skin regeneration.</p>
        <button onclick="addToCart('DermaHeal')">Add to Cart</button>
    </div>
    
    <div class="product" id="dermaGlow">
        <h2>DermaGlow</h2>
        <p>A skincare formula for brightening and scar reduction.</p>
        <button onclick="addToCart('DermaGlow')">Add to Cart</button>
    </div>

    <div id="cart">
        <h2>Shopping Cart</h2>
        <ul id="cart-items"></ul>
        <button onclick="checkout()">Checkout</button>
    </div>

    <script>
        emailjs.init("YOUR_USER_ID");
        let cart = [];

        function addToCart(productName) {
            cart.push(productName);
            updateCart();
        }

        function updateCart() {
            let cartList = document.getElementById("cart-items");
            cartList.innerHTML = "";
            cart.forEach(item => {
                let li = document.createElement("li");
                li.textContent = item;
                cartList.appendChild(li);
            });
        }

        function checkout() {
            if (cart.length === 0) {
                alert("Your cart is empty!");
                return;
            }
            const orderDetails = `Customer ordered: ${cart.join(", ")}`;
            const templateParams = {
                to_email: 'empörteres.girls.guide@gmail.com',
                subject: 'New Order from Kemet Skincare',
                message: orderDetails,
            };

            emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams)
                .then(response => {
                    alert('Your order has been placed successfully!');
                    cart = [];
                    updateCart();
                }, error => {
                    alert('There was an error processing your order. Please try again.');
                });
        }
    </script>
</body>
</html>
