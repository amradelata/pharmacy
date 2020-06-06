<template>
  <div>
    <!-- user states -->
    <div class="home" ref="userstatepopup">
      <div class="hometext">
        <p class="is-size-1">هل انت</p>
        <div class="button is-large is-primary" to="/pharmacyowner" @click="useroner()">مالك صيدلية</div>
        <span class="mideltext">او</span>
        <div class="button is-large is-primary" @click="usercustomer()">مشترى</div>
      </div>
    </div>
    <!-- user states -->
    <!-- loding -->
    <div class="spalsh" ref="splash">
      <div class="lodingContent">
        <h1 class="is-size-1">الصيدليه</h1>
        <img src="~/assets/img/loding.gif" />
        <h3 class="is-size-3">احدث تطبيق يقدم خدمه توصيل العلاج عبر الانترنت</h3>
      </div>
    </div>
    <!-- my app -->
    <div dir="rtl" lang="ar" ref="myApp" class="displayNone">
      <nuxt />
    </div>
  </div>
</template>

<script>
import myVav from "~/components/myVav.vue";
export default {
  data() {
    return {
      userstat: localStorage.getItem("userstat")
    };
  },
  components: {
    myVav
  },
  methods: {
    firstLoding() {
      // console.log(this.$refs["myApp"], this.$refs["splash"]);
      this.$refs["myApp"].style.display = "inline-block";
      this.$refs["splash"].style.display = "none";
    },
    youHaveOrder() {
      this.$refs["newOrder"].classList.toggle("displayNone");
    },
    usercustomer() {
      localStorage.setItem("userstat", "customer");
      this.$router.replace("/customer");
      this.$refs["userstatepopup"].style.display = "none";
    },
    useroner() {
      localStorage.setItem("userstat", "oner");
      this.$router.replace("/pharmacyowner");
      this.$refs["userstatepopup"].style.display = "none";
    }
  },
  mounted() {
    setTimeout(() => {
      this.firstLoding();
    }, 1000);
    //
    // sheck if user state oner open to hem oner page and if user state customer open to hem customer page
    if (this.userstat === null) {
      this.$refs["userstatepopup"].style.display = "block";
    } else if (this.userstat === "oner") {
      this.$router.replace("/pharmacyowner");
      this.$refs["userstatepopup"].style.display = "none";
    } else if (this.userstat === "customer") {
      this.$router.replace("/customer");
      this.$refs["userstatepopup"].style.display = "none";
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

.spalsh {
  background: #191f26;
  color: aliceblue;
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
}
.spalsh h1 {
  color: #25f0ff;
}

.lodingContent {
  position: absolute;
  text-align: center;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
@media screen and (max-width: 768px) {
  .spalsh h3 {
    font-size: 1.25rem !important;
  }
}
</style>
