<template>
  <div>
    <customerNave />
    <div class="mycontainer">
      <ul class="carts" v-if="this.mylocalStorageCard != null" ref="carts">
        <p class="is-size-3">cart item/s {{this.mylocalStorageQty}}</p>

        <li class="cart" v-for="(item,index) in mylocalStorageCard" :key="item.id">
          <div>
            <p class="is-size-6">{{' name : ' + item.tradename}}</p>
            <p class="is-size-6 has-text-success">{{ "price : "+item.price + ' EGP'}}</p>
            {{"qty : "+item.quantity}}
            <div class="cartbuttons"></div>
          </div>
        </li>

        <p
          class="is-size-3 has-text-success"
        >{{' Total price : ' + this.mylocalStorageTolalPrice + " EGP"}}</p>
        <div class="is-size-5 flatshipping">Flat Shipping Credit 10 EGP</div>
        <nuxt-link to="checkout">
          <button class="button" @click="Confirm()">Confirm</button>
        </nuxt-link>
      </ul>
    </div>
  </div>
</template>
<script>
import Swal from "sweetalert2";
import axios from "axios";
import customerNave from "~/components/customerNave.vue";
export default {
  data() {
    return {
      restCart: [],
      drugs: [],
      search: "",
      mylocalStorageCard: [],
      mylocalStorageQty: 0,
      mylocalStorageTolalPrice: 0,
      flatShippingCredit: 10,
      userLatitude: localStorage.getItem("Latitude"),
      userLongitude: localStorage.getItem("Longitude"),
      username: localStorage.getItem("userfirstName"),
      userpassword: localStorage.getItem("userpassword")
    };
  },
  components: { customerNave },
  mounted() {
    //when i refresh  git my cart data from localStorage
    this.mylocalStorageCard = JSON.parse(localStorage.getItem("cart"));
    this.mylocalStorageTolalPrice = localStorage.getItem("totalprice");
    this.mylocalStorageQty = localStorage.getItem("qty");
  },
  methods: {
    //sent cart products to https://pharmacy-databeas.herokuapp.com/User-purchases
    async Confirm() {
      const orderAPI = "https://pharmacy-databeas.herokuapp.com/User-purchases";
      const userorder = [];
      userorder.push(
        this.mylocalStorageCard,

        "totalprice - " +
          (this.mylocalStorageTolalPrice =
            +this.mylocalStorageTolalPrice + +this.flatShippingCredit),
        "cart qty - " + this.mylocalStorageQty,
        "name - " + this.username,
        "userLongitude - " + this.userLongitude,
        "userLatitude - " + this.userLatitude
      );
      // console.log(username);
      const res = await axios.post(orderAPI, userorder);

      //resetcart
      localStorage.setItem("totalprice", 0);
      localStorage.setItem("qty", 0);
      let mystringCart = JSON.stringify(this.restCart); //convert  my array of opject to string to save it on localStorage
      localStorage.setItem("cart", mystringCart);
      window.location.reload();
      this.$refs["carts"].style.display = "none";
    }

    //cart functions
  }
};
</script>

<style scoped>
.mycontainer {
  padding: 0 100px;
  width: 100vw;
}
</style>