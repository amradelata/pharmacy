<template>
  <div class="bell">
    <div class="cards">
      <div class="card">
        <label>السلع المطلوبه</label>
        <br />
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
    <div class="mybutton">
      <nuxt-link to="/acceptinactive">
        <button class="button is-success">قبول</button>
      </nuxt-link>
      <nuxt-link to="/cancel">
        <button class="button is-danger">رفض الطلب</button>
      </nuxt-link>
    </div>
  </div>
</template>


<style scoped>
/* .bell {
  height: 110vh;
} */
.cards {
  display: flex;
  flex-wrap: wrap;
}
.bell {
  position: relative;
  padding: 35px;
}
.bell .mybutton {
  text-align: center;
}
.bell .mybutton button {
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
}
.contnt {
  display: inline-block;
}

.contnt .price {
  color: #6c5ce7;
  font-weight: 900;
}
.qt {
  float: right;
  font-weight: 900;
  margin-top: 80px;
}
.total {
  float: right;
  font-weight: 900;
}
.totalNumper {
  float: left;
  font-weight: 900;
  margin-left: 50px;
  color: #00a8ff;
}
.discrpthintext {
  float: right;
}
@media screen and (max-width: 768px) {
  .bell {
    padding: 0;
  }
  .card {
    width: calc(100% - 20px);
  }

  label {
    font-size: 20px;
  }
}
</style>
