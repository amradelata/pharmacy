<template>
  <div class="acseptOrderTow">
    <myVav />
    <div class="cancel">
      <p class="is-size-1 has-text-success refusetext">قبول الطلب</p>
      <p
        class="is-size-3 refusetextparagraph"
      >برجاء مراجعة الطلب جيدا حيث لا يمكن تعديل الفاتورةاو مدة التوصيل بعد التاكيد</p>
      <div class="radiocard">
        <label>بيانات الفاتورة</label>
        <hr />
        <div class="item">
          <img src="~/assets/img/stopwatch.png" class="img" />
          <span class="spantext">مدة التوصيل</span>
          <span class="spanNumper">30min</span>
        </div>
        <div class="item">
          <img src="~/assets/img/cart.webp" class="img" />
          <span class="spantext">تكلفة الطلب</span>
          <span class="spanNumper">00,00 EGP</span>
        </div>
        <div class="item">
          <img src="~/assets/img/Vespa.png" class="img" />
          <span class="spantext">رسوم التوصيل</span>
          <span class="spanNumper">00,00 EGP</span>
        </div>
        <hr />
        <div class="item">
          <span class="total">المجموع</span>
          <span class="totalNumper">00,00 EGP</span>
        </div>
      </div>
      <div style="text-align: center;">
        <nuxt-link to="/done">
          <button class="button is-light">تاكيد قبول الطلب</button>
        </nuxt-link>
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
.acseptOrderTow {
  background: #1d2c4d;
  padding-bottom: 100px;
}
.cancel {
  text-align: center;
  color: aliceblue;
  /* height: 120vh; */
}
.radiocard {
  text-align: start;
  /* overflow: scroll; */
  position: relative;
  background-color: #fff;
  height: 450px;
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
.item .total {
  color: #000;
  font-size: 25px;
}
.item .totalNumper {
  color: #0984e3;
  font-size: 25px;
  float: left;
}
.item .spanNumper {
  /* display: none; */
  float: left;
}
.item .img {
  width: 30px;
  height: 30px;
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
  .item .img {
    margin-left: 10px;
  }
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