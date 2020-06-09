<template>
  <div>
    <customerNave />
    <div class="orders">
      <div class="cards">
        <div class="card">
          <label>السلع المطلوبه</label>
          <hr />
          <img src="~/assets/img/غسول.png" />
          <div class="contnt">
            <p class="name">Listrine 2</p>
            <span class="price">17,50 EGP</span>
          </div>
          <span class="qt">x1</span>
          <br />
          <hr />
          <img src="~/assets/img/غسول.png" />
          <div class="contnt">
            <p class="name">Listrine</p>
            <span class="price">50,75 EGP</span>
          </div>
          <span class="qt">x1</span>
          <br />
          <hr />
          <span class="total">:المجموع</span>
          <span class="totalNumper">68.25</span>
        </div>
        <div class="card">
          <label>التعليقات المصوره والمكتوبه</label>
          <br />
          <hr />
          <img src="~/assets/img/سيجنالتو.jpg" />
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
    </div>
  </div>
</template>

<script>
import customerNave from "~/components/customerNave.vue";

export default {
  components: {
    customerNave
  }
};
</script>
<style scoped>
.cards {
  display: flex;
  flex-wrap: wrap;
}
.orders {
  position: relative;
  padding: 35px;
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
.contnt .name {
  /* display: inline-block; */
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
  .orders {
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
