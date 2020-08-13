<template>
  <div class="customer" ref="customer">
    <div class="summry" ref="summry"></div>
    <customerNave />
    <!-- map -->
    <div class="map">
      <iframe
        src="https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d13913.965682582799!2d30.86137795!3d29.326590599999996!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sen!2seg!4v1580298588986!5m2!1sen!2seg"
        width="100%"
        height="100%"
        frameborder="0"
        style="border:0;"
        allowfullscreen
      ></iframe>
    </div>
    <!-- map -->

    <div class="ltr">
      <!-- show The nearest pharmacy to the user-->
      <button
        class="button mysearchptn near"
        @click="getyourLocation(),runGetDistance()"
      >اقرب صيدلية</button>

      <!-- search input& button -->
      <div class="field has-addons searchdrug">
        <div class="control" style="width: 100%">
          <input class="input" type="text" placeholder="ابحث عن الدواء" v-model="search" />
        </div>
        <div class="control">
          <a class="button mysearchptn">بحث</a>
        </div>
      </div>
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
        <div class="is-size-5 flatshipping">Flat Shipping Credit 10 EGP</div>
        <button class="button" @click="Confirm(),shownotfcation(),resetcart()">تاكيد الشراء</button>
      </ul>
      <div v-for="item  in drugs" :key="item.id" class="dad">
        <div class="child">
          <div class="mttext">
            <p class="is-size-2 name">{{item.tradename}}</p>
            <p class="is-size-5 price has-text-success">{{ "price : "+item.price + ' EGP'}}</p>
            <p class="is-size-6 color has-text-info">{{item.company}}</p>
            <p class="is-size-5">{{item.pamphlet}}</p>
            <div class="mybuttons">
              <button class="addbutton button is-success" @click="add(i= item.id)">Buy</button>
            </div>
            <button @click="add(i= item.id)" class="buybtnphone button is-success">Buy</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import customerNave from "~/components/customerNave.vue";
import Swal from "sweetalert2";
import axios from "axios";
const API = "https://pharmacy-databeas.herokuapp.com/drugs";
export default {
  components: { customerNave },
  data() {
    return {
      restCart: [],
      drugs: [],
      search: "",
      mylocalStorageCard: [],
      mylocalStorageQty: 0,
      mylocalStorageTolalPrice: 0,
      flatShippingCredit: 10,
      // my fake phrmsy data
      pharmsylocation: [
        { Latitude: "30.039358", Longitude: "31.233043", name: "egypt" },
        { Latitude: "26.817136", Longitude: "36.571405", name: "ksa" },
        { Latitude: "33.334333", Longitude: "10.035706", name: "tunisia" },
        { Latitude: "-8.383071", Longitude: " -56.775322", name: "parasiel" },
        { Latitude: "29.328459", Longitude: " 30.888652", name: "elfyom" },
        { Latitude: "29.325537", Longitude: " 30.854909", name: "myplace" }
      ],
      userLatitude: localStorage.getItem("Latitude"),
      userLongitude: localStorage.getItem("Longitude"),
      username: localStorage.getItem("userfirstName"),
      userpassword: localStorage.getItem("userpassword")
    };
  },
  async created() {
    // show deug data
    const res = await axios.get(API);
    this.drugs = res.data;
    this.drugs = this.drugs.slice(0, 25);
  },
  computed: {
    myresolts() {
      // search
      if (this.search) {
        return this.drugs.filter(item => {
          return item.tradename
            .toLowerCase()
            .includes(this.search.toLowerCase());
        });
      } else {
        console.log("not heare");
      }
    }
  },
  mounted() {
    //when i refresh  git my cart data from localStorage
    this.mylocalStorageCard = JSON.parse(localStorage.getItem("cart"));
    this.mylocalStorageTolalPrice = localStorage.getItem("totalprice");
    this.mylocalStorageQty = localStorage.getItem("qty");
  },
  methods: {
    // get your location
    getyourLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.showPosition);
      } else {
        console.log("Geolocation is not supported by this browser.");
      }
    },
    showPosition(position) {
      localStorage.setItem("Latitude", position.coords.latitude);
      localStorage.setItem("Longitude", position.coords.longitude);
    },
    getDistanceFromLatLonInKm(item) {
      let R = 6371; // Radius of the earth in km
      let dLat = this.deg2rad(item.Latitude - this.userLatitude); // this.deg2rad below
      let dLon = this.deg2rad(item.Longitude - this.userLongitude);
      let a =
        Math.sin(dLat / 2) * Math.sin(dLat / 2) +
        Math.cos(this.deg2rad(this.userLatitude)) *
          Math.cos(this.deg2rad(item.Latitude)) *
          Math.sin(dLon / 2) *
          Math.sin(dLon / 2);
      let c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
      let theDistanceBetweenTwoPlaces = R * c; // Distance in km
      return theDistanceBetweenTwoPlaces;
    },
    deg2rad(deg) {
      return deg * (Math.PI / 180);
    },
    runGetDistance() {
      const arr = this.pharmsylocation.map(this.getDistanceFromLatLonInKm);
      const min = Math.min(...arr);
      console.log(min);
    },
    //cart functions

    async add(i) {
      const addres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/drugs/?id=${i}`
      );

      if (
        this.mylocalStorageCard === null ||
        this.mylocalStorageCard.length === 0
      ) {
        //this is first item in my cart
        this.mylocalStorageCard = [];
        addres.data[0].quantity = 1; //add new key quantity = 1
        this.mylocalStorageCard.push(addres.data[0]); //push this item to my cart opject
        this.mylocalStorageTolalPrice =
          +this.mylocalStorageTolalPrice + +addres.data[0].price;
        this.mylocalStorageQty++;
        //save
        this.savelocalstorage(i);
      } else if (
        this.mylocalStorageCard != null &&
        this.mylocalStorageCard.length > 0
      ) {
        //if this the new item but not the first in cart
        let mystringCartFromLocalStorage = localStorage.getItem("cart"); //get my string cart from localStorage
        let myObject = JSON.parse(mystringCartFromLocalStorage); // return my sting to array of objects
        console.log(myObject);
        const findInMylocalStorageCard = this.mylocalStorageCard.find(
          //search in mylocalStorageCard array of my cliked item
          item => item.id === addres.data[0].id
        );
        if (findInMylocalStorageCard != undefined) {
          //if this item in my cart do not add it again  add to qty ++
          findInMylocalStorageCard.quantity++;
          this.mylocalStorageQty++;

          this.mylocalStorageTolalPrice =
            +this.mylocalStorageTolalPrice + +findInMylocalStorageCard.price;
          //save
          this.savelocalstorage();
        } else {
          //if i have items in my cart but this selected item not found
          addres.data[0].quantity = 1; //add new key quantity = 1
          myObject.push(addres.data[0]); //push this item to my local storedg cart
          this.mylocalStorageCard = myObject; //add my local storedg cart to my cart opject
          this.mylocalStorageTolalPrice =
            +this.mylocalStorageTolalPrice + +addres.data[0].price;
          this.mylocalStorageQty++;
          //save
          this.savelocalstorage(i);
        }
      }
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
    },
    shownotfcation() {
      // start animation delete popup
      Swal.fire({
        title: "تم الطلب بنجاح",
        text: "توقع ان يتم التوصيل فى نصف ساعة "
      });
    },
    resetcart() {
      //this function worck on تاكيد الطب
      localStorage.setItem("totalprice", 0);
      localStorage.setItem("qty", 0);
      let mystringCart = JSON.stringify(this.restCart); //convert  my array of opject to string to save it on localStorage
      localStorage.setItem("cart", mystringCart);
      window.location.reload();
      this.$refs["carts"].style.display = "none";
      // this.$refs["customer"].style.display = "none";
      // this.$refs["summry"].style.display = "block";
    }
    //cart functions
  }
};
</script>

<style  scoped>
.summry {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: #22282f;
  z-index: 999999;
  display: none;
}
.searchdrug {
  margin-bottom: 50px;
}
.ltr {
  direction: ltr;
}
.child {
  position: relative;
  margin: 100px 0;
  padding: 20px 100px 20px 20px;
  cursor: pointer;
}
.mttext {
  padding: 20px;
  z-index: 9999999;
  background: #fff;
  border-radius: 5px;
}
.near {
  margin: 50px 0;
}
.name,
.price {
  display: inline-block;
}
.price {
  margin-left: 100px;
}
.child:hover .mybuttons {
  right: 20px;
  z-index: 50;
  opacity: 1;
  transition: opacity 0.2s;
}
.child:hover .mttext {
  box-shadow: 0 0 38px rgba(117, 117, 115, 0.3), 0 0 0 rgba(220, 235, 14, 0.22);
}
.mybuttons {
  position: absolute;
  top: 20px;
  right: 200px;
  opacity: 0;
  z-index: -1;
}
.addbutton {
  border-radius: 50%;
  width: 60px;
  height: 60px;
  margin: 10px 0;
}
.carts {
  background: #21304f;
  color: aliceblue;
  /* box-shadow: 0 0 38px rgba(117, 117, 115, 0.3), 0 0 0 rgba(220, 235, 14, 0.22); */
  padding: 35px;
  margin-bottom: 100px;
}
.cart {
  box-shadow: 0 0 38px rgba(117, 117, 115, 0.3), 0 0 0 rgba(220, 235, 14, 0.22);
  padding: 20px;
  background: #22282f;
  margin: 20px 0;
}
.cartbuttons {
  margin: 20px 0;
}
.buybtnphone {
  display: none;
}
.flatshipping {
  margin-bottom: 10px;
}
@media screen and (max-width: 768px) {
  .customer {
    overflow-x: hidden;
  }
  .child {
    padding: 0;
    text-align: center;
  }
  .price {
    margin-left: 0;
  }
  .mybuttons {
    display: none;
  }
  .buybtnphone {
    display: block;
    text-align: center;
    width: 100%;
    margin-top: 10px;
  }
}
</style>
