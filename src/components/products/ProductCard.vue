<template>
  <div class="card mb-4 shadow-sm">
    <img :src="product.imageUrl" class="card-img-top product-image" />
    <div class="card-body">
      <h3 class="card-title text-center">{{ product.name }}</h3>
      <h5 class="card-title text-center">{{ product.content }}</h5>

      <div class="row">
        <router-link
          type="button"
          class="btn btn-primary btn-lg"
          :to="'/details/' + product.id"
        >Details</router-link>
      </div>

    </div>
  </div>
</template>

<script>
export default {
    name: "ProductCard",
    props: ["product"]
};
</script>

<style>
.card .product-image {
  height: 300px;
}
.btn {
  border-radius: 0%;
  font-weight: bold;
  background: blueviolet;
  border: black;
  margin: 10px;
}
</style>