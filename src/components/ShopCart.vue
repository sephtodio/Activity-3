<template>
  <div>
    <!-- Product Listings -->
    <div class="product-list">
      <div v-for="product in products" :key="product.id" class="product">
        <p>{{ product.name }} - ₱{{ product.price }}</p>
        <button @click="addToCart(product)">Add to Cart</button>
      </div>
    </div>

    <!-- Shopping Cart -->
    <div class="cart">
      <h2>Shopping Cart</h2>
      <div v-if="cart.length === 0">Cart is empty</div>
      <div v-else>
        <div v-for="(item, index) in cart" :key="index" class="cart-item">
          <p>{{ item.product.name }} - ₱{{ item.product.price }} x {{ item.quantity }}</p>
          <button @click="removeFromCart(index)">Remove</button>
          <input type="number" v-model="item.quantity" min="1" @input="updateQuantity(index)">
        </div>
        <p>Total: ₱{{ totalPrice }}</p>
      </div>
    </div>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      products: [
      { id: 1, name: 'Ball Pen', price: 10 },
          { id: 2, name: 'Pencils', price: 20 },
          { id: 3, name: 'Note Books', price: 30 },
          { id: 4, name: 'Story Books', price: 70 },
          { id: 5, name: 'Glue G', price: 150 },
          { id: 6, name: 'Colors', price: 70 },
          { id: 7, name: 'Boards', price: 150 },
          { id: 8, name: 'Ink Can', price: 200 },
          { id: 9, name: 'Tape V1', price: 10 },
          { id: 10, name: 'Recorder', price: 20 },
          { id: 11, name: 'Horror Book', price: 30 },
          { id: 12, name: 'Index Card', price: 70 },
          { id: 13, name: 'Kit OJT', price: 60 },
          { id: 14, name: 'Glue gun', price: 70 },
          { id: 15, name: 'Desk Int', price: 150 },
          { id: 16, name: 'Retro Tape', price: 200 }
      ],
      cart: []
    };
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => {
        return total + (item.product.price * item.quantity);
      }, 0);
    }
  },
  methods: {
    addToCart(product) {
      const found = this.cart.find(item => item.product.id === product.id);
      if (found) {
        found.quantity++;
      } else {
        this.cart.push({ product: product, quantity: 1 });
      }
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
    },
    updateQuantity(index) {
      const quantity = parseInt(this.cart[index].quantity);
      if (quantity <= 0) {
        this.cart.splice(index, 1);
      }
    }
  }
};
</script>
  
  <style>
  .product-list {
    display: flex;
    flex-wrap: wrap;
  }
  
  .product {
    margin: 9px;
    padding: 10px;
    border: 1px solid #f87a03;
  }
  
  .cart {
    margin-top: 10px;
    background-color: #f87a03;
    text-align: center;
  }
  
  .cart-item {
    margin-bottom: 10px;
  }
  </style>