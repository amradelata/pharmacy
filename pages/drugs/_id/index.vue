<template>
  <div>
    <!--  -->
    <!-- {
    "id": 1,
    "tradename": "1,2,3 (One Two Three) 20 F.C. Tab.",
    "activeingredient": "CHLORPHENIRAMINE+PARACETAMOL(ACETAMINOPHEN)+PSEUDOEPHEDRINE",
    "price": "15",
    "company": "HIKMA PHARMA",
    "group": "",
    "pamphlet": "Indication:\nrunny noses\nblocked noses and sinus\nsneezing\nwatery, itchy eyes\nsinus pain\nfever, headache, body aches & pain\n\ninformation:\nPseudoephedrine hydrochloride belongs to a group of medicines called sympathomimetic decongestants.\nIt works by reducing congestion in the upper respiratory tract, including the nose, nasal passages and sinuses, making it easier to breathe.\nChlorpheniramine maleate belongs to a group of medicines called antihistamines . Antihistamines help reduce allergic symptoms by preventing the effects of a substance called histamine. Histamine is produced by the body in response to foreign substances that the body is allergic to.\nParacetamol works to stop the pain messages from getting through to the brain. It also acts in the brain to reduce fever.",
    "dosage": "",
    "composition": ""
    },-->
    <!--  -->
    <customerNave />
    <div class="mycontainer singlepage">
      <p class="is-size-2 name">{{'Tradename : '+ drugs.tradename}}</p>
      <p class="is-size-6 color has-text-info">{{drugs.company}}</p>
      <p class="is-size-5">{{ 'Pamphlet : ' +this.drugs.pamphlet}}</p>
      <p class="is-size-3 price has-text-success">{{ "price : "+drugs.price + ' EGP'}}</p>

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
import Swal from "sweetalert2";
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

      // this.$router.go();
      this.$router.push("/cart");
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
    // shownotfcation() {
    //   // start animation delete popup
    //   Swal.fire({
    //     position: "top-end",
    //     icon: "success",
    //     title: "Add item to cart",
    //     showConfirmButton: false,
    //     timer: 1500,
    //     html: '<a href="/cart">cart</a>'
    //   });
    // }
  }
};
</script>

<style scoped>
.singlepage {
  background: #fff !important;
  /* direction: ltr; */
  text-align: center;
}
p {
  margin: 50px 35px;
}
</style>