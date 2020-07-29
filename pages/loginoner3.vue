<template>
  <div class="signIn">
    <div class="overlay">
      <div class="signIncards">
        <div class="signIncard">
          <p class="is-size-1 head">صيدلية</p>
          <p class="is-size-3 has-text-black">اول موقع لتوصيل الأدويه فى العالم العربى</p>
        </div>
        <div class="signIncard">
          <div class="myinputs">
            <p class="is-size-3 has-text-black">من فضلك ادخل البيانات التاليه</p>
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
                  placeholder="اسم الصيدليه "
                  v-model="pharmacyName"
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
      // localStorage.setItem("userstate", "oner");
      const nameres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?firstUserName=${this.firstName}`
      );
      const basswordres = await axios.get(
        `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?password=${this.password}`
      );
      console.log(nameres.data, basswordres.data);
      if (nameres.data.length > 0 && basswordres.data.length > 0) {
        this.$router.replace("/pharmacyowner");
      } else if (
        this.password === "" ||
        this.firstName === "" ||
        this.pharmacyName === ""
      ) {
        alert("من فضلك فم بمليء كل البيانات ");
        return;
      } else {
        alert("الرقم السرى  او اسم المستخدم خطأ");
      }
    }
  }
};
</script>

<style  scoped>
.signIn {
  /* background-image: url("https://image.freepik.com/free-vector/abstract-health-medical-science-consist-dna_36402-305.jpg") !important; */
  background-position: center center;
  background-size: cover;
  text-align: center;
  position: relative;
  height: 100vh;
  width: 100vw;
}
.overlay {
  position: absolute;
  /* background: #0000009c; */
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
}
.myinputs {
  margin-top: -50px;
}
.head {
  color: #00d1b2;
}
.signIncards input {
  margin: 15px 0;
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

.mybuttons button {
  margin-right: 35px;
  /* width: 250px; */
}
.control {
  text-align: center;
}
@media screen and (max-width: 768px) {
  .signIn {
    /* background-image: none; */
    height: 120vh;
  }

  /* .overlay {
    background: #fff;
  } */
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
}
</style>