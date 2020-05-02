<template>
  <div class="container">
    <div class="cancel">
      <p class="is-size-1 has-text-danger refusetext">رفض الطلب</p>
      <p
        class="is-size-3 refusetextparagraph"
      >لكى نتمكن من تحسين الخدمه و جعلها بشكل افضل . برجاء تحديد سبب الغاء الطلب</p>
      <div class="radiocard">
        <label>لماذا تم رفض الطلب</label>
        <hr />
        <div class="item">
          <input type="checkbox" />
          <span>الدواء المطلوب غير متوافر فى الصيدليه</span>
        </div>
        <div class="item">
          <input type="checkbox" />
          <span>الطلب يحتوى على مواد مخدرة</span>
        </div>
        <div class="item">
          <input type="checkbox" />
          <span>الطلب غير واضح</span>
        </div>
        <div class="item">
          <input type="checkbox" />
          <span>المكان خارجنطاق التوصيل</span>
        </div>
        <div class="item">
          <input type="checkbox" />
          <span>اسباب اخرى</span>
        </div>

        <div class="control">
          <textarea class="textarea"></textarea>
        </div>
      </div>
      <div style="text-align: center;">
        <nuxt-link to="/cancel">
          <button class="button is-danger">رفض الطلب</button>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<style scoped>
.cancel {
  text-align: center;
  color: aliceblue;
  height: 120vh;
}
.radiocard {
  text-align: start;
  overflow: scroll;
  position: relative;
  background-color: #fff;
  height: 400px;
  color: #000;
  padding: 35px;
  width: calc(50% - 20px);
  margin: 10px;
  display: inline-block;
  box-shadow: 0 0 38px rgba(117, 117, 115, 0.3), 0 0 0 rgba(220, 235, 14, 0.22);
}

.item {
  margin: 35px 0;
}
.item span {
  padding: 0 30px;
}
.cancel button {
  width: 50%;
  margin-bottom: 20px;
}
.refusetext {
  padding: 35px 0;
}
.refusetextparagraph {
  padding: 35px 0;
}

@media screen and (max-width: 768px) {
  .cancel button {
    width: 95%;
    margin-bottom: 20px;
  }
  .radiocard {
    width: calc(100% - 20px);
  }
  .item span {
    padding: 0;
  }
  .refusetext {
    font-size: 35px !important;
    padding: 10px 0;
  }
  .refusetextparagraph {
    font-size: 15px !important;
    padding: 10px 0;
  }
}
</style>