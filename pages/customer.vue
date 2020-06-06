<template>
  <div>
    <customerNave />
    <!-- map -->
    <div class="map">
      <iframe
        src="https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d13913.965682582799!2d30.86137795!3d29.326590599999996!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sen!2seg!4v1580298588986!5m2!1sen!2seg"
        width="100%"
        frameborder="0"
        style="border:0;"
        allowfullscreen
      ></iframe>
    </div>
    <!-- map -->

    <div class="container">
      <!-- show The nearest pharmacy to the user-->
      <button class="button mysearchptn" @click="getyourLocation(),runGetDistance()">اقرب صيدلية</button>
      <!-- search input& button -->
      <div class="field has-addons">
        <div class="control" style="width: 100%">
          <input class="input" type="text" placeholder="ابحث عن الدواء" v-model="search" />
        </div>
        <div class="control">
          <a class="button mysearchptn">بحث</a>
        </div>
      </div>
      <!-- my cards -->
      <div class="cards">
        <div v-for="(item,index) in drugs" :key="item.id" class="card">
          <!-- <div v-for="(item,index) in myresolts" :key="item.id" class="card"> -->
          <p class="is-size-5">{{'Trade Name : ' + item.tradename}}</p>
          <br />
          <br />
          <p class="is-size-6">{{'Price : ' + item.price + ' EG'}}</p>
          <br />
          <button class="button is-info" @click="order(index,item.id) ,shownotfcation()">طلب</button>
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
      drugs: [],
      search: "",
      pharmsylocation: [
        { Latitude: "30.039358", Longitude: "31.233043", name: "egypt" },
        { Latitude: "26.817136", Longitude: "36.571405", name: "ksa" },
        { Latitude: "33.334333", Longitude: "10.035706", name: "tunisia" },
        { Latitude: "-8.383071", Longitude: " -56.775322", name: "parasiel" },
        { Latitude: "29.328459", Longitude: " 30.888652", name: "elfyom" },
        { Latitude: "29.325537", Longitude: " 30.854909", name: "myplace" }
      ],
      userLatitude: localStorage.getItem("Latitude: "),
      userLongitude: localStorage.getItem("Longitude: ")
    };
  },
  async created() {
    const res = await axios.get(API);
    this.drugs = res.data;
    this.drugs = this.drugs.slice(0, 25);
    // console.log(this.drugs)
  },
  computed: {
    myresolts() {
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
  methods: {
    async order(index) {
      const orderAPI = "https://pharmacy-databeas.herokuapp.com/User-purchases";
      const res = await axios.post(orderAPI, this.drugs[index]);
      // console.log(this.drugs[index])
      // this.posts.push(res.data)
    },
    shownotfcation() {
      // start animation delete popup
      Swal.fire({
        title: "تم الطلب بنجاح",
        text: "توقع ان يتم التوصيل فى نصف ساعة "
      });
    },
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
    }
  }
};
</script>

<style scoped>
.cards {
  display: flex;
  flex-wrap: wrap;
}
.card {
  flex-basis: calc(25% - 20px);
  display: inline-block;
  margin: 10px;
  border-radius: 5px;
  box-shadow: 0 0 38px rgba(117, 117, 115, 0.3), 0 0 0 rgba(220, 235, 14, 0.22);
  padding: 35px;
  cursor: pointer;
  text-align: center;
}
.input {
  margin: 20px auto;
}
.map iframe {
  height: 100vh;
}
.mysearchptn {
  margin-top: 20px;
  color: #fff;
  background: #3298dc;
  /* padding: 0; */
  border-radius: 0 !important;
}
@media screen and (max-width: 768px) {
  .card {
    flex-basis: calc(100% - 20px);
  }
}
</style>