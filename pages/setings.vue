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
          <div class="itemleft">{{pharmsyInformation.name}}</div>
        </div>
        <div class="item">
          <div class="itemright">الرقم الساخن</div>
          <div class="itemleft">{{pharmsyInformation.hotligh}}</div>
        </div>
        <div class="suphead">
          <span>عنوان الفرع</span>
        </div>
        <div class="item">
          <div class="itemright">المدينة</div>
          <div class="itemleft">{{pharmsyInformation.city}}</div>
        </div>
        <div class="item">
          <div class="itemright">المنطقة</div>
          <div class="itemleft">{{pharmsyInformation.region}}</div>
        </div>
        <div class="item">
          <div class="itemright">الشارع</div>
          <div class="itemleft">{{pharmsyInformation.street}}</div>
        </div>
        <div class="item">
          <div class="itemright">رقم المبنى</div>
          <div class="itemleft">{{pharmsyInformation.buildingNumber}}</div>
        </div>
        <div class="item">
          <div class="itemright">اتساع مساحه التوصيل</div>
          <div class="itemleft">{{pharmsyInformation.breadthOfTheConnectionSpace + ' كيلو'}}</div>
        </div>
        <!-- <div class="item">
          <div class="itemright">موقعك</div>
          <div class="itemleft">19°56’56.96″S 69°38’1.83″W</div>
        </div>-->
        <div class="item">
          <div class="itemright">خطوط الطول</div>
          <div class="itemleft">{{pharmsyInformation.Latitude}}</div>
        </div>
        <div class="item">
          <div class="itemright">حطوط العرض</div>
          <div class="itemleft">{{pharmsyInformation.Longitude}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import myVav from "~/components/myVav.vue";
import axios from "axios";
const userpharmsylocation =
  "https://pharmacy-databeas.herokuapp.com/pharmacy-Information";

export default {
  components: {
    myVav
  },
  data() {
    return {
      pharmsyInformation: [],
      pharmacyName: localStorage.getItem("myPharmacyName")
    };
  },

  async created() {
    // search in all pharmacy with this pharmacy name
    const res = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/pharmacy-Information/?name=${this.pharmacyName}`
    );
    this.pharmsyInformation = res.data[0];
    console.log(res.data[0]);
    console.log(this.myuser);
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