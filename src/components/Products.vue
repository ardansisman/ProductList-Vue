<template>
  <div class="row product-container">
<app-product v-for="product in productList">
    <img class="card-img-top" :src="
            product.selectedImage == null
              ? '/src/assets/default.png'
              : product.selectedImage
          " alt="Card image cap">
        <div class="card-body">
          <h5 class="card-title">{{product.title}}</h5>
          <small>
            <strong>Adet : </strong> {{ product.count }}
          </small>
          <br>
          <small>
            <strong>Fiyat : </strong> {{ product.price }}
          </small>
          <br>
          <small>
            <strong>Tutar : </strong> {{ product.totalPrice}}
          </small>
        </div>
</app-product>

  </div>
</template>

<script>
import Product from "./Product.vue"
import { eventBus } from "../main";
export default {
    components:{
        appProduct : Product
    },
    data(){
        return {
            productList : [],
        }
    },
    created(){
      eventBus.$on("productAdded", (product) => {
        if (this.productList.length < 10 ) {
        this.productList.push(product); 
          eventBus.$emit("progressbarUpdated",this.productList.length);
        }else{
          alert("Ürün sepete eklenemez");
        }
      });
    }
};
</script>
