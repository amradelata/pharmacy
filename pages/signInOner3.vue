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
            <p class="is-size-3">انشاء حساب مالك صيدلية</p>
            <!--putons  -->
            <div class="mybuttons">
              <!-- inptus -->
              <div class="field">
                <div class="control">
                  <!-- <nuxt-link to="/logIn">
              <button class="button  is-outlined">تسجيل الدخول</button>
            </nuxt-link>

            <nuxt-link to="/signIn">
              <button class="button  is-outlined">حساب جديد</button>
                  </nuxt-link>-->
                  <input class="input" type="text" placeholder="الاسم " v-model="firstUserName" />
                  <input class="input" type="text" placeholder="هاتف المستخدم" v-model="userphone" />
                  <input class="input" type="text" placeholder="الرقم السرى" v-model="password" />

                  <input class="input" type="text" placeholder="البريد" v-model="email" />
                  <input
                    class="input"
                    type="text"
                    placeholder="اسم الصيدلية"
                    v-model="pharmacyName"
                  />
                  <input
                    class="input"
                    type="text"
                    placeholder="الخط الساخن"
                    v-model="pharmacyhotligh"
                  />
                  <input class="input" type="text" placeholder="المدينة" v-model="pharmacycity" />

                  <input class="input" type="text" placeholder="المنطقة" v-model="pharmacyregion" />
                  <input class="input" type="text" placeholder="الشارع" v-model="pharmacystreet" />
                  <input
                    class="input"
                    type="text"
                    placeholder="رقم المبنى"
                    v-model="pharmacybuildingNumber"
                  />
                  <input
                    class="input"
                    type="text"
                    placeholder="اتساع مساحه التوصيل"
                    v-model="pharmacybreadthOfTheConnectionSpace"
                  />
                  <!-- <input
                    class="input"
                    type="text"
                    placeholder="خطوط الطول- موقعك"
                    v-model="pharmacyLongitude"
                  />
                  <input
                    class="input"
                    type="text"
                    placeholder="حطوط العرض- موقعك"
                    v-model="pharmacyLatitude"
                  />-->
                  <!--  -->
                  <!-- <div class="control">
              <p>نوع الحساب</p>
              <label class="radio">
                <input type="radio" name="foobar" @click="useroner()" />
                <p class="is-size-6">مشترى</p>
              </label>
              <label class="radio">
                <input type="radio" name="foobar" @click="usercustomer()" />
                <p class="is-size-6">مالك صيدلية</p>
              </label>
                  </div>-->
                  <!--  -->
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
const pharmacyInformation =
  "https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information";
export default {
  data() {
    return {
      firstUserName: "",
      userphone: "",
      email: "",
      password: "",
      pharmacyName: "",
      pharmacyhotligh: "",
      pharmacycity: "",
      pharmacyregion: "",
      pharmacystreet: "",
      pharmacybuildingNumber: "",
      pharmacybreadthOfTheConnectionSpace: "",
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
    // usercustomer() {
    //   this.userstat = "oner";

    //   console.log(this.userstat);
    // },
    // useroner() {
    //   this.userstat = "customer";
    //   console.log(this.userstat);
    // },
    async submit() {
      const mypharmacyName = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?firstUserName=${this.firstUserName}`
      );
      if (mypharmacyName.data.length > 0) {
        alert("هذا الاسم موجود بالفعل ");
        return;
      } else if (
        this.firstUserName === "" ||
        this.userphone === "" ||
        this.password === "" ||
        this.email === "" ||
        this.pharmacyName === "" ||
        this.pharmacyhotligh === "" ||
        this.pharmacycity === "" ||
        this.pharmacyregion === "" ||
        this.pharmacystreet === "" ||
        this.pharmacybuildingNumber === "" ||
        this.pharmacybreadthOfTheConnectionSpace === "" ||
        this.pharmacyLatitude === ""
      ) {
        alert("من فضلك فم بمليء كل البيانات ");
        return;
      }
      const res = await axios.post(pharmacyInformation, {
        firstUserName: this.firstUserName,
        email: this.email,
        password: this.password,
        userphone: this.userphone,
        pharmacyName: this.pharmacyName,
        pharmacyhotligh: this.pharmacyhotligh,
        city: this.pharmacycity,
        region: this.pharmacyregion,
        street: this.pharmacystreet,
        buildingNumber: this.pharmacybuildingNumber,
        breadthOfTheConnectionSpace: this.pharmacybreadthOfTheConnectionSpace,
        userstat: "oner",
        Latitude: this.pharmacyLongitude,
        Longitude: this.pharmacyLatitude
      });
      console.log(res);
      localStorage.setItem("userstat", "oner");
      localStorage.setItem("userfirstName", this.firstUserName);
      localStorage.setItem("useremail", this.email);
      localStorage.setItem("userpassword", this.password);
      localStorage.setItem("pharmacyName", this.pharmacyName);
      this.$router.replace("/pharmacyowner");

      const useracount = localStorage.getItem("userstat");
      if (useracount == "customer") {
        this.$router.replace("/customer");
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
  /* background: #0000009c; */
  top: 10%;
  bottom: 0;
  right: 0;
  left: 0;
  transform: translate(0, -10%);
}

.head {
  color: #00d1b2;
}
.signIncards {
  display: flex;
  flex-wrap: wrap;
  /* margin-right: 20px; */
  text-align: center;
  /* margin-top: 10%; */
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
  /* display: inline-block;
  width: 300px; */
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
}
</style>