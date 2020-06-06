<template>
  <div>
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
    }
  },
  mounted() {
    setTimeout(() => {
      this.firstLoding();
    }, 1000);
  }
};
</script>
<style  scoped>
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