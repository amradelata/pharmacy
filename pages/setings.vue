<template>
  <div>
    <myVav />
    <div class="container">
      <div class="setings">
        <div class="head">
          <span class="itemright">اعدادات الصفحه</span>
          <button class="itemleft button is-rounded">حفظ</button>
        </div>
        <div class="suphead">
          <span>بيانات الصيدليه</span>
        </div>
        <div class="item itemimg">
          <div class="itemright">شعار الصيدليه</div>
          <div class="itemleft">
            <img src="https://placeimg.com/100/100/any" />
          </div>
        </div>
        <div class="item">
          <div class="itemright">اسم الصيدليه</div>
          <div class="itemleft">El zreher</div>
        </div>
        <div class="item">
          <div class="itemright">الرقم الساخن</div>
          <div class="itemleft">90010</div>
        </div>
        <div class="suphead">
          <span>عنوان الفرع</span>
        </div>
        <div class="item">
          <div class="itemright">المدينه</div>
          <div class="itemleft">القاهره</div>
        </div>
        <div class="item">
          <div class="itemright">المنطقة</div>
          <div class="itemleft">وسط البلد</div>
        </div>
        <div class="item">
          <div class="itemright">الشارع</div>
          <div class="itemleft">محمد على</div>
        </div>
        <div class="item">
          <div class="itemright">رقم المبنى</div>
          <div class="itemleft">16</div>
        </div>
        <div class="item">
          <div class="itemright">اتساع مساحه التوصيل</div>
          <div class="itemleft">3 كيلو</div>
        </div>
        <div class="item">
          <div class="itemright">موقعك</div>
          <div class="itemleft">19°56’56.96″S 69°38’1.83″W</div>
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

.setings {
  /* text-align: center; */
  color: aliceblue;
  width: 100%;
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