<template>
  <div>
    <!-- loding -->
    <div class="spalsh" ref="splash">
      <div class="lodingContent">
        <!-- <h1 class="is-size-1">الصيدليه</h1> -->
        <img src="~/assets/img/loding.gif" />
        <!-- <h3 class="is-size-3">احدث تطبيق يقدم خدمه توصيل العلاج عبر الانترنت</h3> -->
      </div>
    </div>
    <!-- my app -->
    <div dir="rtl" lang="ar" ref="myApp" class="displayNone">
      <myVav />
      <notification />
      <div class="map">
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d13913.965682582799!2d30.86137795!3d29.326590599999996!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sen!2seg!4v1580298588986!5m2!1sen!2seg"
          width="100%"
          height="100%"
          frameborder="0"
          style="border:0;"
          allowfullscreen
        ></iframe>
      </div>
    </div>
  </div>
</template>

<script>
import myVav from "~/components/myVav.vue";
import notification from "~/components/notification.vue";

export default {
  components: {
    myVav,
    notification
  },
  methods: {
    firstLoding() {
      console.log(this.$refs["myApp"], this.$refs["splash"]);
      this.$refs["myApp"].style.display = "inline-block";
      this.$refs["splash"].style.display = "none";
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
body {
  font-family: "Cairo", sans-serif;
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
/* .spalsh h1 {
  color: #25f0ff;
} */

.lodingContent {
  position: absolute;
  text-align: center;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
@media screen and (max-width: 768px) {
}
</style>