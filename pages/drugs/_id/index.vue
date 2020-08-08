<template>
  <div class="mttext">
    <customerNave />
    <div class="mycontainer">
      <p class="is-size-2 name">{{drugs.tradename}}</p>
      <p class="is-size-5 price has-text-success">{{ "price : "+drugs.price + ' EGP'}}</p>

      <p class="is-size-6 color has-text-info">{{drugs.company}}</p>
      <p class="is-size-5">{{this.drugs.pamphlet}}</p>
      <div class="mybuttons">
        <!-- <nuxt-link to="/cart"> -->
        <button class="addbutton button is-success" @click="add( i = drugs.id )">add to cart</button>
        <!-- </nuxt-link> -->
      </div>
      <!-- <button @click="add(i= this.drugs.id)" class="buybtnphone button is-success">More</button> -->
    </div>
  </div>
</template>

<script>
import axios from "axios";
import customerNave from "~/components/customerNave.vue";
export default {
  components: { customerNave },
  data() {
    return {
      id: this.$route.params.id,
      drugs: [],
      mylocalStorageCard: [],
      mylocalStorageQty: 0,
      mylocalStorageTolalPrice: 0
    };
  },
  async created() {
    const res = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/drugs/${this.id}`
    );
    this.drugs = res.data;
    console.log(this.drugs);
  },
  mounted() {
    //when i refresh  git my cart data from localStorage
    this.mylocalStorageCard = JSON.parse(localStorage.getItem("cart"));
    this.mylocalStorageTolalPrice = localStorage.getItem("totalprice");
    this.mylocalStorageQty = localStorage.getItem("qty");
  },
  methods: {
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
        this.savelocalstorage();
      } else if (
        this.mylocalStorageCard != null &&
        this.mylocalStorageCard.length > 0
      ) {
        //if this the new item but not the first in cart
        let mystringCartFromLocalStorage = localStorage.getItem("cart"); //get my string cart from localStorage
        let myObject = JSON.parse(mystringCartFromLocalStorage); // return my sting to array of objects
        console.log(this.mylocalStorageCard);
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
          this.savelocalstorage();
        }
      }

      this.$router.go();
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
    }
  }
};
</script>

<style scoped>
.mycontainer {
  padding: 0 100px;
}
</style>