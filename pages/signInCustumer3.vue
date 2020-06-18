<template>
  <div>
    <!-- user states -->
    <div class="home">
      <div class="hometext">
        <p class="is-size-1 has-text-black">من فضلك ادخل البيانات التاليه</p>
        <!-- inptus -->
        <div class="field">
          <div class="control">
            <input class="input is-primary" type="text" placeholder="الاسم" v-model="name" />
            <input class="input is-primary" type="text" placeholder="الايميل" v-model="email" />

            <input
              class="input is-primary"
              type="text"
              placeholder="الرقم السرى"
              v-model="password"
            />
            <input
              class="input is-primary"
              type="text"
              placeholder="رقم الهاتف"
              v-model="userphone"
            />

            <input
              class="input is-primary"
              type="text"
              placeholder="حطوط العرض- موقعك"
              v-model="pharmacyLatitude"
            />
            <input
              class="input is-primary"
              type="text"
              placeholder="خطوط الطول- موقعك"
              v-model="pharmacyLongitude"
            />

            <button class="button is-primary" @click="submit()">تسجيل الدخول</button>
          </div>
        </div>

        <!-- inptus -->
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
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
      pharmacyLatitude: ""
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
        this.firstName === "" ||
        this.email === "" ||
        this.password === "" ||
        this.userphone === "" ||
        this.Latitude === "" ||
        this.Longitude === ""
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

      // localStorage.setItem("userstat", "customer");
      localStorage.setItem("userfirstName", this.name);
      //   localStorage.setItem("userfirstName", this.firstName);
      //   localStorage.setItem("userlastName", this.lastName);
      //   localStorage.setItem("useremail", this.email);
      //   localStorage.setItem("userpassword", this.password);
      //   localStorage.setItem("userstat", this.userstat);
      this.$router.replace("/customer");
      // const useracount = localStorage.getItem("userstat");
      // if (useracount == "customer") {
      // } else if (useracount == "oner") {
      //   this.$router.replace("/pharmacyowner");
      // }
    }
  }
};
</script>

<style  scoped>
.home {
  text-align: center;
  position: relative;
  height: 100vh;
  width: 100vw;
}
.home input {
  margin: 15px 0;
}
.home p {
  margin-bottom: 25px;
  color: aliceblue;
}
.mideltext {
  font-size: 45px;
  color: aliceblue;
  margin: 0 35px;
}
.hometext {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.radio {
  text-align: center;
  margin: 0 25px;
}
@media screen and (max-width: 768px) {
  .mideltext {
    display: block;
    margin: 35px;
  }
}
</style>