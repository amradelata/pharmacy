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
    <!-- <button class="button mysearchptn near" @click="getyourLocation(),runGetDistance()">اقرب صيدلية</button> -->

    <div class="mycontainer">
      <ul class="cards">
        <li class="card" v-for="item in drugs" :key="item.id">
          <nuxt-link :to="'/drugs/' + item.id">
            <p class="is-size-4">{{item.tradename}}</p>
            <p class="is-size-6 has-text-primary">{{"price : "+item.price + ' EGP'}}</p>
          </nuxt-link>
        </li>
      </ul>
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
    this.drugs = this.drugs.slice(0, 24);
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
    // get your location
    // get Your nearest pharmacy
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
    // get Your nearest pharmacy
  }
};
</script>

<style scoped>
.mycontainer {
  width: 100vw;
  padding: 35px 100px;
  background: #192a56;
}
.cards {
  display: flex;
  flex-wrap: wrap;
  /* padding: 0 35px; */
  /* width: 100% */
}
.card {
  flex-basis: calc(33.333% - 20px);
  display: inline-block;
  margin: 10px;
  overflow: hidden;
  padding: 20px;
  text-align: center;
}
@media screen and (max-width: 768px) {
  .card {
    flex-basis: calc(100% - 20px);
  }
  .mycontainer {
    padding: 35px 10px;
  }
}
</style>