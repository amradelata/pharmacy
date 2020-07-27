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
                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="اسمك"
                    v-model="firstName"
                  />

                  <input
                    class="input is-primary"
                    type="text"
                    placeholder="الرقم السرى"
                    v-model="password"
                  />

                  <button class="button is-primary" @click="submit()">تسجيل الدخول</button>
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
const usersArray =
  "https://pharmacy-databeas.herokuapp.com/userCustomer-information";
export default {
  data() {
    return {
      password: "",
      firstName: ""
    };
  },
  methods: {
    async submit() {
      localStorage.setItem("userpassword", this.password);
      localStorage.setItem("userfirstName", this.firstName);
      localStorage.setItem("myPharmacyName", this.pharmacyName);
      const nameres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/userCustomer-information/?firstName=${this.firstName}`
      );
      const basswordres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/userCustomer-information/?password=${this.password}`
      );
      console.log(nameres.data, basswordres.data);
      if (nameres.data.length > 0 && basswordres.data.length > 0) {
        this.$router.replace("/customer");
      } else {
        alert("الرقم السرى  او اسم المستخدم خطأ");
      }
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
  margin: 15px 0;
}

.mybuttons button {
  margin-right: 35px;
  width: 250px;
}
.myinputs {
  margin-top: -50px;
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