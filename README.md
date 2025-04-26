# Planerwear<!DOCTYPE html><html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PlanetWear</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js" defer></script>
  <script src="https://checkout.razorpay.com/v1/checkout.js"></script>
  <style>
    body {
      background: linear-gradient(to right, #1e3c72, #2a5298);
    }
    header, footer {
      background: rgba(0, 0, 0, 0.7);
    }
    h1, h2, h3, p, a, button, span {
      color: #f1f5f9;
    }
    .planet-card {
      background: rgba(255, 255, 255, 0.1);
      backdrop-filter: blur(5px);
    }
  </style>
</head>
<body class="text-white" x-data="shopApp()">
  <header class="shadow">
    <div class="container mx-auto px-6 py-4 flex justify-between items-center">
      <h1 class="text-2xl font-bold">PlanetWear</h1>
      <nav>
        <ul class="flex space-x-6">
          <li><a href="#" class="hover:text-yellow-300">Home</a></li>
          <li><a href="#" class="hover:text-yellow-300">Shop</a></li>
          <li><a href="#" class="hover:text-yellow-300">About</a></li>
          <li><a href="#" class="hover:text-yellow-300">Contact</a></li>
          <li>
            <button class="hover:text-yellow-300 relative">
              Cart (<span x-text="cart.length"></span>)
            </button>
          </li>
        </ul>
      </nav>
    </div>
  </header>  <section class="py-12">
    <div class="container mx-auto px-6 text-center">
      <h2 class="text-4xl font-bold mb-4 text-yellow-300">Planet-Inspired Styles</h2>
      <p class="mb-6 text-gray-200">Wear the universe. Explore cosmic fashion.</p>
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
        <template x-for="product in products">
          <div class="planet-card p-4 rounded shadow">
            <img :src="product.image" :alt="product.name" class="w-full h-64 object-cover rounded mb-4">
            <h3 class="text-lg font-semibold" x-text="product.name"></h3>
            <p class="text-sm text-gray-300" x-text="product.description"></p>
            <p class="text-yellow-300 font-bold">₹<span x-text="product.price"></span></p>
            <button class="mt-2 px-4 py-2 bg-yellow-500 text-black rounded hover:bg-yellow-600" @click="addToCart(product)">Add to Cart</button>
          </div>
        </template>
      </div>
    </div>
  </section>  <section class="py-8" x-show="cart.length > 0">
    <div class="container mx-auto px-6">
      <h3 class="text-2xl font-bold mb-4 text-yellow-300">Your Cart</h3>
      <ul class="space-y-2">
        <template x-for="(item, index) in cart" :key="index">
          <li class="flex justify-between items-center bg-gray-800 p-2 rounded">
            <span x-text="item.name"></span>
            <span>₹<span x-text="item.price"></span></span>
          </li>
        </template>
      </ul>
      <div class="mt-4 text-right font-bold text-yellow-300">Total: ₹<span x-text="total()"></span></div>
      <button class="mt-4 px-6 py-2 bg-green-500 text-black rounded hover:bg-green-600" @click="payNow">
        Checkout
      </button>
    </div>
  </section>  <footer class="shadow mt-12">
    <div class="container mx-auto px-6 py-4 text-center">
      <p class="text-gray-400">&copy; 2025 PlanetWear. All rights reserved.</p>
    </div>
  </footer>  <script>
    function shopApp() {
      return {
        cart: [],
        products: [
          { name: 'Mars T-Shirt', price: 499, image: 'https://via.placeholder.com/300?text=Mars', description: 'Bold red tee inspired by the red planet.' },
          { name: 'Saturn Hoodie', price: 1299, image: 'https://via.placeholder.com/300?text=Saturn', description: 'Ringed planet vibes in cozy comfort.' },
          { name: 'Jupiter Jacket', price: 899, image: 'https://via.placeholder.com/300?text=Jupiter', description: 'Stormy style from the gas giant.' },
          { name: 'Neptune Kurti', price: 799, image: 'https://via.placeholder.com/300?text=Neptune', description: 'Cool tones and galactic grace.' }
        ],
        addToCart(product) {
          this.cart.push(product);
        },
        total() {
          return this.cart.reduce((t, p) => t + p.price, 0);
        },
        payNow() {
          const options = {
            key: "YOUR_KEY_ID",
            amount: this.total() * 100,
            currency: "INR",
            name: "PlanetWear",
            description: "Clothing Purchase",
            handler: function (response) {
              alert("Payment successful! Payment ID: " + response.razorpay_payment_id);
            },
            prefill: {
              name: "Pulkit",
              email: "customer@example.com",
              contact: "9999999999"
            },
            theme: {
              color: "#facc15"
            }
          };
          const rzp = new Razorpay(options);
          rzp.open();
        }
      }
    }
  </script></body>
</html>
