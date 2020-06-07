<template>
  <div>
    <myVav />
    <div class="container">
      <div class="setingsuser">
        <div class="head">
          <span class="itemright">الحساب</span>
          <button class="itemleft button is-rounded">حفظ</button>
        </div>
        <div class="suphead">
          <span>بيانات الخصوصية</span>
        </div>
        <div class="item">
          <div class="itemright">الاسم</div>
          <div class="itemleft">Amr Adel Ata</div>
        </div>
        <div class="item">
          <div class="itemright">الرقم الهاتف</div>
          <div class="itemleft">90010</div>
        </div>

        <div class="item">
          <div class="itemright">البريد</div>
          <div class="itemleft">amradelata@gmail.com</div>
        </div>
        <div class="item">
          <div class="itemright">تعديل كلمة السر</div>
          <div class="itemleft">></div>
        </div>
        <div style="text-align: center; padding: 100px 20px">
          <nuxt-link to="/cancel">
            <button class="button is-light" style="width: 100%">نسجيل الخروج</button>
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import myVav from "~/components/myVav.vue";

export default {
  components: {
    myVav
  }
};
</script>

<style scoped>
.head {
  padding: 50px 0;
}

.setingsuser {
  color: aliceblue;
  height: 100vh;
}
.itemright,
.itemleft {
  display: inline-block;
}
.item {
  border-bottom: 1px solid #cccccc38;
  position: relative;
  padding: 20px 0;
}
.itemright {
  text-align: start;
}
.itemleft {
  position: absolute;
  left: 0;
}
.suphead {
  background: #e2e2e2;
  padding: 15px;
  color: #000;
}
.itemimg {
  padding: 100px 0;
  padding-top: 30px;
}
@media screen and (max-width: 768px) {
  .itemright {
    padding-right: 20px;
  }

  .itemleft {
    left: 20px;
  }
}
</style>