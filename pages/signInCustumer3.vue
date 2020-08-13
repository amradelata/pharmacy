<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard slogan">
          <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3 has-text-black">اول موقع لتوصيل الأدويه فى العالم العربى</p>
        </div>
        <div class="signIncard">
          <div class="myinputs">
            <img
              class="inputimg"
              src="https://static.dribbble.com/users/1769954/screenshots/7367730/media/60163f104190cf8b2097bdba6b0fab5a.png"
              alt
            />
            <p class="is-size-3">انشاء حساب مشترى</p>
            <!--putons  -->
            <div class="mybuttons">
              <!-- inptus -->
              <div class="field">
                <div class="control">
                  <input class="input" type="text" placeholder="الاسم" v-model="name" />
                  <input class="input" type="text" placeholder="الايميل" v-model="email" />

                  <input class="input" type="text" placeholder="الرقم السرى" v-model="password" />
                  <input class="input" type="text" placeholder="رقم الهاتف" v-model="userphone" />

                  <!-- <input
                    class="input"
                    type="text"
                    placeholder="حطوط العرض- موقعك"
                    v-model="pharmacyLatitude"
                  />
                  <input
                    class="input"
                    type="text"
                    placeholder="خطوط الطول- موقعك"
                    v-model="pharmacyLongitude"
                  />-->
                  <button
                    class="button mysearchptn near"
                    @click="getyourLocation(),runGetDistance(),shownotfcation()"
                  >الحصول على موقعك</button>
                  <button class="button is-primary" @click="submit()">تسجيل الحساب</button>
                </div>
              </div>

              <!-- inptus -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Swal from "sweetalert2";
const usersArray =
  "https://pharmacy-databeas.herokuapp.com/userCustomer-information";
export default {
  data() {
    return {
      userphone: "",
      password: "",
      email: "",
      name: "",
      pharmacyLongitude: "",
      pharmacyLatitude: "",
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
      userLongitude: localStorage.getItem("Longitude")
    };
  },
  methods: {
    async submit() {
      const nameres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/userCustomer-information/?firstName=${this.name}`
      );
      if (nameres.data.length > 0) {
        alert("هذا الاسم موجود بالفعل ");
        return;
      } else if (
        this.name === "" ||
        this.email === "" ||
        this.password === "" ||
        this.userphone === "" ||
        this.pharmacyLatitude === ""
      ) {
        alert("من فضلك فم بمليء كل البيانات ");
        return;
      } else {
        const res = await axios.post(usersArray, {
          firstName: this.name,
          email: this.email,
          password: this.password,
          userphone: this.userphone,
          userstat: "customer",
          Latitude: this.pharmacyLatitude,
          Longitude: this.pharmacyLongitude
        });
      }

      localStorage.setItem("userstat", "customer");
      localStorage.setItem("useremail", this.email);
      localStorage.setItem("userpassword", this.password);
      localStorage.setItem("userfirstName", this.name);

      this.$router.replace("/drugs");

      const useracount = localStorage.getItem("userstat");
      if (useracount == "customer") {
      } else if (useracount == "oner") {
        this.$router.replace("/pharmacyowner");
      }
    },
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
      let Latitude = localStorage.getItem("Latitude");
      let Longitude = localStorage.getItem("Longitude");
      this.pharmacyLatitude = Latitude;
      this.pharmacyLongitude = Longitude;
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
    },
    // get Your nearest pharmacy
    shownotfcation() {
      // start animation delete popup
      Swal.fire({
        title: "تم الحصول على موقعك ",
        text: "كل بياناتك يتم حفظها فى سرية تامة"
      });
    }
  }
};
</script>

<style  scoped>
.signIn {
  position: absolute;
  top: 50%;
  bottom: 0;
  right: 0;
  left: 0;
  transform: translate(0, -50%);
}

.head {
  color: #00d1b2;
}
.signIncards {
  display: flex;
  flex-wrap: wrap;
  /* margin-right: 20px; */
  text-align: center;
  /* margin-top: 20%; */
}

.signIncard {
  flex-basis: calc(50% - 20px);
  display: inline-block;
  background-color: transparent;
  margin: 10px;
  padding: 10px;
  color: #fff;
}
.signIncards input {
  margin: 5px 0;

  /* width: 250px; */
}

.mybuttons button {
  /* margin-right: 35px; */
}
.myinputs {
  background-color: #40407e;
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
  padding: 20px 50px;
}
.inputimg {
  width: 100px;
}
.control {
  text-align: center;
}
.slogan {
  padding: 100px 0;
}
@media screen and (max-width: 768px) {
  .overlay {
    position: absolute;
    top: 20%;
    transform: translate(0, -20%);
  }
  .signIn {
    /* height: 100vh; */
  }
  .signIncards {
    margin-right: 0;
  }
  .signIncard {
    flex-basis: calc(100% - 10px);
  }
  .mybuttons button {
    margin-right: 0;
    margin-top: 20px;
  }
  .myinputs {
    margin-top: 0;
  }
  .slogan {
    padding: 0;
  }
  .signIn {
    margin-top: 35px;
    position: absolute;
    top: 0%;
    bottom: 0;
    right: 0;
    left: 0;
    transform: translate(0, -0%);
  }
}
</style>