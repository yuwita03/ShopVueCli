<template>
  <nav class="navbar navbar-light fixed-top" >
        <div class="navbar-text ml-auto d-flex" >
          <button class="btn btn-sm btn-outline-succes btn-success" @click="$emit('toggle')">
          <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
          </button>
          <div class="dropdown ml-2 " v-if="cart.length > 0">
            <button class="btn btn-sm btn-outline-success dropdown-toggle" id="dropdownCart" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
              <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
                <span class="badge badge-pill badge-success">{{ cartQty }}</span>
                <price :value="Number(cartTotal)"></price>
            </button>
            <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownCart">
              <div v-for="(item, index) in cart" :key="index">
                <div class="dropdown-item-text text-nowrap text-right">
                  <span class="badge badge-pill badge-warning align-text-top">
                    {{ item.qty }}
                  </span>
                  {{ item.product.name }}
                  <b class="mr-2">{{ item.product.price * item.qty| currencyFormat }}</b>
                  <a href="#" class="badge badge-danger text-white" v-on:click.stop="deleteItem(index)">-</a>
                </div>
              </div>
            </div>
          </div>
        </div>
    </nav>
</template>
<script>
    import Price from "./Price.vue"; 
    import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";

    export default{
        name: "navbar",
        props: ["cart", "cartQty", "cartTotal"],
        component: {
          Price,
          FontAwesomeIcon
        },
        filters: {
            currencyFormat: function(value){
            return 'Rp' + Number.parseFloat(value).toFixed(2);
    }
  },
}
</script>