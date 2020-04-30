<template>
  <div>
    <div class="btncontaner">
      <button
        ref="cangemybtn"
        @click="togelnotification()"
        class="button is-medium is-fullwidth mybtn"
      >متصل</button>
    </div>

    <div class="notification is-primary" ref="primary">انت الان تسطاتيع استقبال الطلبات</div>
    <div
      class="notification is-danger displayNone"
      ref="danger"
    >انت غير متصل لن تتمكن من استقبال الطلبات</div>
  </div>
</template>
<script>
export default {
  methods: {
    togelnotification() {
      this.$refs["primary"].classList.toggle("displayNone");
      this.$refs["danger"].classList.toggle("displayNone");

      var x = this.$refs["cangemybtn"];
      if (x.innerHTML === "متصل") {
        x.innerHTML = "غير متصل";
      } else {
        x.innerHTML = "متصل";
      }
    }
  }
};
</script>