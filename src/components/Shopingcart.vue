<template>
    <div>
      <h1>Shopping Cart</h1>
      <div>
        <h2>Products</h2>
        <ul>
          <li v-for="(product, index) in products" :key="index">
            {{ product.name }} - ${{ product.price }}
            <button @click="addToCart(index)">Add to Cart</button>
          </li>
        </ul>
      </div>
      <div>
        <h2>Cart</h2>
        <ul>
          <li v-for="(item, index) in cart" :key="index">
            {{ item.name }} - ${{ item.price }} - Quantity: {{ item.quantity }}
            <button @click="removeFromCart(index)">Remove</button>
            <button @click="increaseQuantity(index)">+</button>
            <button @click="decreaseQuantity(index)">-</button>
          </li>
        </ul>
        <p>Total: ${{ total }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        products: [
        { id: 1, name: 'PIZZA', price: 100 },
          { id: 2, name: 'BURGER', price: 30 },
          { id: 3, name: 'SHAWARMA', price: 70 },
          { id: 4, name: 'CORNDOG', price: 25 },
          { id: 5, name: 'FRENCHFRIES', price: 40},
          { id: 6, name: 'POPCORN', price: 15 }
        ],
        cart: []
      };
    },
    computed: {
      total() {
        return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
      }
    },
    methods: {
      addToCart(index) {
        const productToAdd = this.products[index];
        const existingItemIndex = this.cart.findIndex((item) => item.name === productToAdd.name);
        if (existingItemIndex !== -1) {
          this.cart[existingItemIndex].quantity++;
        } else {
          this.cart.push({ ...productToAdd, quantity: 1 });
        }
      },
      removeFromCart(index) {
        this.cart.splice(index, 1);
      },
      increaseQuantity(index) {
        this.cart[index].quantity++;
      },
      decreaseQuantity(index) {
        if (this.cart[index].quantity > 1) {
          this.cart[index].quantity--;
        }
      }
    }
  };
  </script>
  <style>
  ul{list-style-type: none;}
</style>