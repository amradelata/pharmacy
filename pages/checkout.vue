<template>
  <div>
    <customerNave />
    <div class="mycontainer checkout">
      <ul class="carts" v-if="this.mylocalStorageCard != null" ref="carts">
        <p class="is-size-3">cart item/s {{this.mylocalStorageQty}}</p>

        <li class="cart" v-for=" item in mylocalStorageCard" :key="item.id">
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

        <!--  -->
        <input
          ref="flatcredit"
          type="radio"
          id="flatcredit"
          name="shipping"
          value="flatcredit"
          @click="flatcredit()"
        />
        <label for="flatcredit">Flat Shipping Credit 10 EGP</label>
        <br />
        <input
          type="radio"
          id="LocalPickup"
          name="shipping"
          value="LocalPickup"
          ref="LocalPickup"
          @click="LocalPickup()"
        />
        <label for="LocalPickup">Local pickup</label>
        <!--  -->
        <nuxt-link to="checkout">
          <button class="button Confirmptn" @click="Confirm()">Confirm</button>
          <!-- <button @click="search()">sdasdasd</button> -->
        </nuxt-link>
      </ul>
    </div>
  </div>
</template>
<script>
import Swal from "sweetalert2";
import axios from "axios";
import customerNave from "~/components/customerNave.vue";
const usersArray =
  "https://pharmacy-databeas.herokuapp.com/userCustomer-information";
export default {
  data() {
    return {
      restCart: [],
      drugs: [],

      mylocalStorageCard: [],
      mylocalStorageQty: 0,
      mylocalStorageTolalPrice: 0,
      // flatShippingCredit: 10,
      myshipping: false,
      userLatitude: localStorage.getItem("Latitude"),
      userLongitude: localStorage.getItem("Longitude"),
      username: localStorage.getItem("userfirstName"),
      userpassword: localStorage.getItem("userpassword"),
      myusersArray: [],
      myallopjects: {},
      tradename: "",
      price: 0,
      quantity: 0
    };
  },
  components: { customerNave },
  mounted() {
    //when i refresh  git my cart data from localStorage
    this.mylocalStorageCard = JSON.parse(localStorage.getItem("cart"));
    this.mylocalStorageTolalPrice = localStorage.getItem("totalprice");
    this.mylocalStorageQty = localStorage.getItem("qty");
    console.log(this.username);
  },
  async created() {
    console.log(this.username);
    const res = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/userCustomer-information?firstName=${this.username}`
    );
    this.myusersArray = res.data[0]; //get th user who user name = this.username
    // console.log(this.myusersArray);
  },
  methods: {
    flatcredit() {
      this.myshipping ^= true; // set myshipping  to true
      if (this.myshipping === 1) {
        this.mylocalStorageTolalPrice = +this.mylocalStorageTolalPrice + +10;

        this.$refs["flatcredit"].disabled = true;
        this.$refs["LocalPickup"].disabled = false;
      }
    },
    LocalPickup() {
      // this.myshipping = false;
      if (this.myshipping === 0) {
        this.mylocalStorageTolalPrice = +this.mylocalStorageTolalPrice + -0;

        this.$refs["LocalPickup"].disabled = true;
        this.$refs["flatcredit"].disabled = false;
      } else if (this.myshipping === 1) {
        this.mylocalStorageTolalPrice = +this.mylocalStorageTolalPrice + -10;
        this.$refs["LocalPickup"].disabled = true;
        this.$refs["flatcredit"].disabled = false;
      }
    },

    //sent cart products to https://pharmacy-databeas.herokuapp.com/User-purchases-information
    // search() {
    //   let x = this.mylocalStorageCard.map(this.tradename);
    //   console.log(x);
    // },
    async Confirm() {
      // console.log(myusername);
      localStorage.setItem("totalprice", this.mylocalStorageTolalPrice); // save my shipping credet
      const orderinformationAPI =
        "https://pharmacy-databeas.herokuapp.com/User-purchases-information";
      const ordercartAPI =
        "https://pharmacy-databeas.herokuapp.com/User-purchases-cart";
      // let totalArry = [
      //   "totalprice - " + this.mylocalStorageTolalPrice,
      //   "cart qty - " + this.mylocalStorageQty
      // ];
      // const userorderInformation = totalArry.concat(
      //   this.myusersArray,
      //   this.mylocalStorageCard
      // );

      this.mylocalStorageCard.forEach(async function(arryitem) {
        //
        const myusername = localStorage.getItem("userfirstName");
        const res = await axios.get(
          `https://pharmacy-databeas.herokuapp.com/userCustomer-information?firstName=${myusername}`
        );
        const username = res.data[0].firstName;
        const useremail = res.data[0].email;
        const userphone = res.data[0].userphone;
        const userLongitude = res.data[0].Longitude;
        const userLatitude = res.data[0].Latitude;

        console.log(username);
        //
        const usercart = {
          tradename: arryitem.tradename,
          price: arryitem.price,
          quantity: arryitem.quantity,
          username: username,
          useremail: useremail,
          userphone: userphone,
          userLongitude: userLongitude,
          userLatitude: userLatitude
        };
        console.log(usercart);
        const myres = await axios.post(ordercartAPI, usercart);
      });
      const userorderInformation = {
        TolalPrice: this.mylocalStorageTolalPrice,
        qty: this.mylocalStorageQty,
        name: this.myusersArray.firstName,
        email: this.myusersArray.email,
        phone: this.myusersArray.userphone,
        Longitude: this.myusersArray.Longitude,
        Latitude: this.myusersArray.Latitude
      };
      // const usercart = this.mylocalStorageCard;

      // console.log(userorderInformation);
      // console.log(this.mylocalStorageTolalPrice);

      const res = await axios.post(orderinformationAPI, userorderInformation);

      // //resetcart
      // localStorage.setItem("totalprice", 0);
      // localStorage.setItem("qty", 0);
      // let mystringCart = JSON.stringify(this.restCart); //convert  my array of opject to string to save it on localStorage
      // localStorage.setItem("cart", mystringCart);
      // window.location.reload();
      // this.$refs["carts"].style.display = "none";
    }
    // shownotfcation() {
    //   // start animation delete popup
    //   Swal.fire({
    //     title: "تم الطلب بنجاح"
    //   });
    // }

    //cart functions
  }
};
</script>

<style scoped>
.Confirmptn {
  display: block;
  margin: 35px 0;
}
.checkout {
  background: #fff !important;
  direction: ltr;
}
.cart {
  border: 1px solid #000;
  margin: 35px 0;
  padding: 20px;
  background: #273c75;
  color: #fff;
}
</style>