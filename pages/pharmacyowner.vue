<template>
  <div>
    <myVav />
    <notification />
    <!-- map -->
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
    <!-- map -->

    <!--  simulate-->
    <!-- <div style="text-align: center; padding: 35px">
      <button class="button is-warning" @click="youHaveOrder()">simulate i have order</button>
    </div>-->

    <!-- displayNone -->
    <div class="newOrder" ref="newOrder">
      <div class="cards">
        <div class="card">
          <label>السلع المطلوبه</label>
          <hr />
          <!-- <img src="~/assets/img/غسول.png" /> -->
          <div class="contnt" v-for="item in orders" :key="item.id">
            <p class="name">{{item.tradename}}</p>
            <span class="price">{{item.price}} EGP</span>
            <p class="qty">{{'عدد : '+item.quantity}}</p>
          </div>
          <span class="qt">{{' عدد المنتجات الكلى : ' + this.qty}}</span>
          <br />
          <hr />

          <br />
          <hr />
          <span class="total">:المجموع</span>
          <span class="totalNumper">{{this.totalprice}}</span>
        </div>
        <div class="card">
          <label>التعليقات المصوره والمكتوبه</label>
          <br />
          <hr />
          <!-- <img src="~/assets/img/سيجنالتو.jpg" /> -->
          <br />
          <hr />
          <p class="discrpthintext">محتاج معجون اسنان سجنل تو او المسواك</p>
        </div>
        <div class="card">
          <label>توصيل الى</label>
          <br />
          <hr />
          <p class="discrpthintext">16 شارع سعد زغلول</p>
        </div>
      </div>
      <div class="mybutton">
        <nuxt-link to="/acceptinactive">
          <button class="button is-success">قبول</button>
        </nuxt-link>
        <nuxt-link to="/cancel">
          <button class="button is-danger">رفض الطلب</button>
        </nuxt-link>
      </div>
    </div>
  </div>
  <!--  simulate-->
</template>
<script>
import notification from "~/components/notification.vue";
import myVav from "~/components/myVav.vue";
import Axios from "axios";

export default {
  data() {
    return {
      orders: [],
      qty: 0,
      totalprice: 0
    };
  },
  components: {
    notification,
    myVav
  },
  methods: {
    youHaveOrder() {
      this.$refs["newOrder"].classList.toggle("displayNone");
    }
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
.qty,
.price,
.name {
  margin: 10px 0;
}
.name {
  font-size: 20px;
}
.cards {
  display: flex;
  flex-wrap: wrap;
}
.newOrder {
  position: relative;
  padding: 35px;
}
.newOrder .mybutton {
  text-align: center;
}
.newOrder .mybutton button {
  margin: 35px 0;
  font-size: 20px;
  width: 150px;
}
.card {
  direction: ltr;
  padding: 35px;
  width: calc(33.333% - 20px);
  margin: 10px;
  display: inline-block;
  box-shadow: 0 0 38px rgba(117, 117, 115, 0.3), 0 0 0 rgba(220, 235, 14, 0.22);
}
label {
  float: right;
  font-size: 25px;
}
.card img {
  width: 100px;
  /* text-align: center; */
  /* display: inline-block; */
}
.contnt {
  display: inline-block;
}
.contnt .price {
  /* display: block; */
  color: #6c5ce7;
  font-weight: 900;
}
.qt {
  /* display: block; */
  float: right;
  font-weight: 900;
  /* margin-right: 50px; */
  margin-top: 80px;
}
.total {
  /* display: block; */
  float: right;
  font-weight: 900;
  /* margin-right: 50px; */
}
.totalNumper {
  /* display: block; */
  float: left;
  font-weight: 900;
  margin-left: 50px;
  color: #00a8ff;
}
.discrpthintext {
  /* display: block; */
  float: right;
}
@media screen and (max-width: 768px) {
  .newOrder {
    padding: 0;
  }
  .card {
    width: calc(100% - 20px);
    /* text-align: center; */
    /* padding: 35px 50px 35px 0; */
  }
  label {
    font-size: 20px;
  }
}
</style>
