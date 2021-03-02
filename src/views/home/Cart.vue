<template>
  <div class="container" style="padding: 30px">
    <div class="row d-flex justify-content-center">
      <div class="list-group col-8">
        <a
          v-for="item in cart"
          :key="item.id"
          href="#"
          class="list-group-item list-group-item-action d-flex justify-content-between align-items-center"
        >
          <div class="col-3">
            <label class="sr-only" for="inlineFormInputName2">Quantity</label>
            <input
              type="number"
              v-model="quantity"
              class="form-control mb-2 mr-sm-2"
            />
            <button
              v-if="!isInCardProp"
              @click.stop="addCart({ product, quantity })"
              type="button"
              class="btn btn-primary btn-lg btn-block col-9"
            >
              ADD
            </button>
            <button
              v-else
              @click.stop="removeCart(product.id)"
              type="button"
              class="btn btn-primary btn-lg btn-block col-9"
            >
              REMOVE
            </button>
          </div>
          <img :src="item.imageUrl" alt height="60" width="60" />
          <p class="h4">{{ item.name }}</p>
          <div class="row">
            <div class="mr-2">
              <p>Unique Price</p>
              <p>${{ item.price }}</p>
            </div>
            <div class="mr-2">
              <p>Total Price</p>
              <p>${{ item.price * item.quantity }}</p>
            </div>
            <div>
              <p>Quantity</p>
              <p>{{ item.quantity }}</p>
            </div>
          </div>
        </a>
        <div
          class="list-group-item list-group-item-action d-flex justify-content-between align-items-center"
        >
          <p class="h4">Total</p>
          <div>
            <p>Total Price</p>
            <p>${{ totalPrice }}</p>
          </div>
        </div>
        <button
          @click="checkout()"
          type="button"
          class="btn btn-primary btn-lg btn-block mt-4"
        >
          Checkout
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions, mapState } from "vuex";
export default {
  name: "Cart",
  data() {
    return {
      totalPrice: 0,
      isInCardProp: false,
    };
  },
  computed: {
    ...mapGetters("product", ["cart"]),
    ...mapGetters("product", ["product"]),
    ...mapState("product", ["cart"]),
  },
  
  methods: {
    
    ...mapActions("product", ["removeCart"]),
    calcPrice() {
      this.cart.forEach((element) => {
        this.totalPrice += element.price * element.quantity;
      });
    },
    checkout() {
      const vm = this;
      setTimeout(() => {
        vm.removeCart();
        alert("Purchase successful!");
        vm.$router.push("/");
      }, 2000);
    },
    isInCart(id) {
      for (let index = 0; index < this.cart.length; index++) {
        const element = this.cart[index];
        if (element.id === id) {
          return true;
        }
      }
      return false;
    },
  },
  watch: {
    product(val) {
      this.isInCardProp = this.isInCart(val.id);
    },
    cart() {
      this.isInCardProp = this.isInCart(this.product.id);
    },
    quantity(val) {
      if (val <= 0) {
        this.quantity = 1;
      }
    },

  },
  mounted() {
    this.calcPrice();
  },
};
</script>

<style>
</style>
