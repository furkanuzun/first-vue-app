<template>
  <div v-if="productList.length > 0">
    <h3 class="text-center">Eklenen Ürünlerin Listesi</h3>
    <hr>
    <div class="row product-container">
      <app-product v-for="product in productList">
        <img class="card-img-top" :src="product.selectedImage" alt="Card image cap">
        <div class="card-body">
          <h5 class="card-title">{{ product.title }}</h5>
          <small>
            <strong>Adet :</strong>
            {{product.count}}
          </small>
          <br>
          <small>
            <strong>Fiyat :</strong>
            {{product.price}}
          </small>
          <br>
          <small>
            <strong>Tutar :</strong>
            {{product.totalPrice}}
          </small>
        </div>
      </app-product>
    </div>
  </div>
</template>
<script>
import Product from "./Product";
import { eventBus } from "../main.js";

export default {
  components: {
    appProduct: Product
  },
  data() {
    return {
      maxProduct : 10,
      productList: []
    };
  },
  created() {
    eventBus.$on("productAdded", product => {
      if (this.productList.length < this.maxProduct) {
        this.productList.push(product);
        eventBus.$emit("productListLength", this.productList.length);
      } else {
        alert("Daha fazla ürün ekleyemezsiniz.");
      }
    });
  }
};
</script>
