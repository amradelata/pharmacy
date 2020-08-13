<template>
  <div class="acseptOrderOne">
    <myVav />
    <div class="done mycontainer">
      <p class="is-size-1 has-text-success refusetext">قبول الطلب</p>
      <p
        class="is-size-3 refusetextparagraph"
      >برجاء مراجعة الطلب جيدا حيث لا يمكن تعديل الفاتورةاو مدة التوصيل بعد التاكيد</p>
      <div class="radiocard">
        <label>بيانات الفاتورة</label>
        <hr />

        <div class="myitem">
          <!-- <img src="~/assets/img/cart.webp" class="img" /> -->
          <span class="spantext">تكلفة الطلب</span>
          <span class="spanNumper">{{this.totalprice +' EGP'}}</span>
        </div>

        <div class="item">
          <span class="total">المجموع</span>
          <span class="totalNumper">{{this.totalprice +' EGP'}}</span>
        </div>
      </div>
      <div style="text-align: center;">
        <nuxt-link to="/">
          <button class="button is-success">تاكيد قبول الطلب</button>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>
<script>
import myVav from "~/components/myVav.vue";
import Axios from "axios";
export default {
  components: {
    myVav
  },
  data() {
    return {
      orders: [],
      qty: 0,
      totalprice: 0
    };
  },
  async created() {
    const orderAPI = "https://pharmacy-databeas.herokuapp.com/User-purchases";
    const res = await Axios.get(orderAPI);
    this.orders = res.data;
    this.orders = this.orders[1][0];
    this.totalprice = res.data[1][1];
    this.qty = res.data[1][2];
    console.log(this.orders);
  }
};
</script>
<style scoped>
.acseptOrderOne {
  background: #1d2c4d;
  padding-bottom: 100px;
}
.done {
  text-align: center;
  color: aliceblue;
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
.myitem {
  text-align: center !important;
}
.myitem .spanNumper {
  display: block;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 20px;
  margin-top: 20px;
}
.myitem .img {
  width: 30px;
  height: 30px;
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
.done button {
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
  .done button {
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