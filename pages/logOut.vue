<template>
  <div class="logout">
    <myVav />

    <!-- user states -->
    <div class="home">
      <div class="hometext">
        <p class="is-size-1">هل تريد تسجيل الخروج</p>
        <button class="button is-large is-primary" @click="logout()">حسناً</button>
      </div>
    </div>
    <!-- user states -->
  </div>
</template>

<script>
import myVav from "~/components/myVav.vue";
export default {
  components: {
    myVav
  },
  methods: {
    logout() {
      localStorage.setItem("userpassword", null);
      localStorage.setItem("userfirstName", null);
      localStorage.setItem("myPharmacyName", null);
      this.$router.replace("/");
    }
  }
};
</script>

<style  scoped>
.logout {
  background: #1d2c4d;
}
.home {
  text-align: center;
  position: relative;
  height: 95vh;
  width: 100vw;
}
.home p {
  margin-bottom: 100px;
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
@media screen and (max-width: 768px) {
  .mideltext {
    display: block;
    margin: 35px;
  }
}
</style>