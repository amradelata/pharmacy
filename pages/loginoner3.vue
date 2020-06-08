<template>
  <div>
    <!-- user states -->
    <div class="home">
      <div class="hometext">
        <!-- inptus -->
        <div class="field">
          <div class="control">
            <input class="input is-primary" type="text" placeholder="اسمك" v-model="firstName" />

            <input
              class="input is-primary"
              type="text"
              placeholder="الرقم السرى"
              v-model="password"
            />
            <input
              class="input is-primary"
              type="text"
              placeholder="اسم الصيدليه  اذا كنت صاحب الصيدليه فقط"
              v-model="pharmacyName"
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
  "https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information";
export default {
  data() {
    return {
      password: "",
      firstName: "",
      pharmacyName: ""
    };
  },
  methods: {
    async submit() {
      localStorage.setItem("userpassword", this.password);
      localStorage.setItem("userfirstName", this.firstName);
      localStorage.setItem("myPharmacyName", this.pharmacyName);
      const nameres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?firstUserName=${this.firstName}`
      );
      const basswordres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?password=${this.password}`
      );
      console.log(nameres.data, basswordres.data);
      if (nameres.data.length > 0 && basswordres.data.length > 0) {
        this.$router.replace("/");
      } else {
        alert("الرقم السرى  او اسم المستخدم خطأ");
      }
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