<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard">
          <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3">اول موقع لتوصيل الأدويه فى العالم العربى</p>
        </div>
        <div class="signIncard">
          <div class="myinputs">
            <p class="is-size-3">من فضلك ادخل البيانات التاليه</p>
            <!--putons  -->
            <div class="mybuttons">
              <!-- inptus -->
              <div class="field">
                <div class="control">
                  <!-- <nuxt-link to="/logIn">
              <button class="button is-primary is-outlined">تسجيل الدخول</button>
            </nuxt-link>

            <nuxt-link to="/signIn">
              <button class="button is-primary is-outlined">حساب جديد</button>
                  </nuxt-link>-->
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="الاسم "
                    v-model="firstUserName"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="هاتف المستخدم"
                    v-model="userphone"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="الرقم السرى"
                    v-model="password"
                  />

                  <input class="input is-primary" type="text" placeholder="البريد" v-model="email" />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="اسم الصيدلية"
                    v-model="pharmacyName"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="الخط الساخن"
                    v-model="pharmacyhotligh"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="المدينة"
                    v-model="pharmacycity"
                  />

                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="المنطقة"
                    v-model="pharmacyregion"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="الشارع"
                    v-model="pharmacystreet"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="رقم المبنى"
                    v-model="pharmacybuildingNumber"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="اتساع مساحه التوصيل"
                    v-model="pharmacybreadthOfTheConnectionSpace"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="خطوط الطول- موقعك"
                    v-model="pharmacyLongitude"
                  />
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="حطوط العرض- موقعك"
                    v-model="pharmacyLatitude"
                  />
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
      pharmacyLatitude: ""
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
        this.userphone === "" ||
        this.firstUserName === "" ||
        this.email === "" ||
        this.pharmacyName === "" ||
        this.pharmacyhotligh === "" ||
        this.city === "" ||
        this.region === "" ||
        this.street === "" ||
        this.buildingNumber === "" ||
        this.breadthOfTheConnectionSpace === "" ||
        this.Latitude === "" ||
        this.Longitude === "" ||
        this.firstUserName === ""
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
      // localStorage.setItem("userstat", "oner");
      localStorage.setItem("userfirstName", this.firstUserName);
      // localStorage.setItem("userfirstName", this.firstName);
      // localStorage.setItem("userlastName", this.lastName);
      // localStorage.setItem("useremail", this.email);
      // localStorage.setItem("userpassword", this.password);
      // localStorage.setItem("userstat", this.userstat);
      this.$router.replace("/pharmacyowner");
      // const useracount = localStorage.getItem("userstat");
      // if (useracount == "customer") {
      //   this.$router.replace("/customer");
      // } else if (useracount == "oner") {
      //   this.$router.replace("/pharmacyowner");
      // }
    }
  }
};
</script>

<style  scoped>
.signIn {
  background-image: url("https://image.freepik.com/free-vector/abstract-health-medical-science-healthcare-icon_36402-276.jpg") !important;
  background-position: center center;
  background-size: cover;
  text-align: center;
  position: relative;
  height: 100vh;
  width: 100vw;
}
.overlay {
  position: absolute;
  background: #0000009c;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
}
.head {
  color: #00d1b2;
}
.signIncards {
  display: flex;
  flex-wrap: wrap;
  margin-right: 20px;
  margin-top: 20%;
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
  display: inline-block;
  width: 300px;
}

.mybuttons button {
  margin-right: 35px;
  width: 250px;
}
.myinputs {
  margin-top: -100px;
}

@media screen and (max-width: 768px) {
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
}
</style>