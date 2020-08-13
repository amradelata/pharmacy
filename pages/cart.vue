<template>
  <div>
    <customerNave />
    <div class="mycontainer cartpage">
      <ul class="carts" v-if="this.mylocalStorageCard != null" ref="carts">
        <p class="is-size-3">cart item/s {{this.mylocalStorageQty}}</p>

        <li class="cart" v-for="(item,index) in mylocalStorageCard" :key="item.id">
          <div>
            <p class="is-size-6">{{' name : ' + item.tradename}}</p>
            <p class="is-size-6 has-text-success">{{ "price : "+item.price + ' EGP'}}</p>
            {{"qty : "+item.quantity}}
            <div class="cartbuttons">
              <button
                class="cartbutton button is-success"
                @click="mydelete(i = item.id, index)"
              >delete</button>
              <button class="cartbutton button is-success" @click="addtoquantty(i = item.id)">+</button>

              <button
                v-if="item.quantity"
                class="cartbutton button is-success"
                @click="removefromquantty(i = item.id, index)"
              >-</button>
            </div>
          </div>
        </li>

        <p
          class="is-size-3 has-text-success"
        >{{' Total price : ' + this.mylocalStorageTolalPrice + " EGP"}}</p>
        <!-- <div class="is-size-5 flatshipping">Flat Shipping Credit 10 EGP</div> -->
        <nuxt-link to="checkout">
          <button class="button">Proceed to checkout</button>
        </nuxt-link>

        <button @click="refreshpage()" class="button">update cart</button>
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
    refreshpage() {
      this.$router.go(); // refresh page with vue way
    },
    addtoquantty(i) {
      const myclickdObject = this.mylocalStorageCard.find(
        item => item.id === i
      );
      console.log(this.mylocalStorageTolalPrice);
      myclickdObject.quantity++;
      this.mylocalStorageQty++;

      this.mylocalStorageTolalPrice =
        +this.mylocalStorageTolalPrice + +myclickdObject.price;

      // save
      this.savelocalstorage();
    },
    removefromquantty(i, index) {
      const myclickdObject = this.mylocalStorageCard.find(
        item => item.id === i
      );

      myclickdObject.quantity--;
      this.mylocalStorageQty--;

      this.mylocalStorageTolalPrice =
        +this.mylocalStorageTolalPrice + -myclickdObject.price;
      if (myclickdObject.quantity === 0) {
        this.mylocalStorageCard.splice(index, 1);
      }
      //save
      this.savelocalstorage();
    },
    mydelete(i, index) {
      const myclickdObject = this.mylocalStorageCard.find(
        item => item.id === i
      );

      this.mylocalStorageCard.splice(index, 1);
      this.mylocalStorageTolalPrice =
        +this.mylocalStorageTolalPrice +
        -myclickdObject.price * myclickdObject.quantity;
      this.mylocalStorageQty =
        +this.mylocalStorageQty + -myclickdObject.quantity;
      //save
      this.savelocalstorage();
    },
    savelocalstorage() {
      // localStorage
      localStorage.setItem("totalprice", this.mylocalStorageTolalPrice);
      localStorage.setItem("qty", this.mylocalStorageQty);
      let mystringCart = JSON.stringify(this.mylocalStorageCard); //convert  my array of opject to string to save it on localStorage
      localStorage.setItem("cart", mystringCart); //set cart string
      // localStorage
    },
    //sent cart products to https://pharmacy-databeas.herokuapp.com/User-purchases
    async Confirm() {
      const orderAPI = "https://pharmacy-databeas.herokuapp.com/User-purchases";
      const userorder = [];
      userorder.push(
        this.mylocalStorageCard,

        (this.mylocalStorageTolalPrice =
          +this.mylocalStorageTolalPrice + +this.flatShippingCredit),
        "cart qty - " + this.mylocalStorageQty,
        "name - " + this.username,
        "userLongitude - " + this.userLongitude,
        "userLatitude - " + this.userLatitude
      );
      // console.log(username);
      const res = await axios.post(orderAPI, userorder);
    }

    //cart functions
  }
};
</script>

<style scoped>
.cart {
  border: 1px solid #000;
  margin: 35px 0;
  padding: 20px;
  background: #273c75;
  color: #fff;
}
.cartbuttons {
  margin: 20px 0;
}
.cartpage {
  background: #fff !important;
  direction: ltr;
}
</style>