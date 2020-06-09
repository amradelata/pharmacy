<template>
  <div>
    <myVav />
    <div class="container">
      <div class="setings">
        <div class="head">
          <span class="itemright">اعدادات الصفحه</span>
          <button class="itemleft button is-rounded" @click="seave()">حفظ</button>
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
          <div class="itemleft">{{pharmsyInformation.pharmacyName}}</div>
        </div>
        <!--  -->

        <!-- <div class="item">
          <div class="itemright">الرقم الصيدلية</div>
          <div class="itemleft">{{pharmsyInformation.pharmacyhotligh}}</div>
        </div>-->

        <!--  -->
        <div class="item">
          <div @click="showeditpharmacyhotligh()" class="items">
            <div class="itemright">الرقم الصيدلية</div>
            <div class="itemleft">{{pharmsyInformation.pharmacyhotligh}}</div>
          </div>

          <div class="edit" ref="editpharmacyhotligh">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.pharmacyhotligh"
              ref="pharmacyhotlighinput"
            />
          </div>
        </div>
        <div class="suphead">
          <span>عنوان الفرع</span>
        </div>
        <!-- <div class="item">
          <div class="itemright">المدينة</div>
          <div class="itemleft">{{pharmsyInformation.city}}</div>
        </div>-->

        <div class="item">
          <div @click="showeditpharmacycity()" class="items">
            <div class="itemright">المدينة</div>
            <div class="itemleft">{{pharmsyInformation.city}}</div>
          </div>

          <div class="edit" ref="editpharmacycity">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.city"
              ref="pharmacycityinput"
            />
          </div>
        </div>
        <!-- <div class="item">
          <div class="itemright">المنطقة</div>
          <div class="itemleft">{{pharmsyInformation.region}}</div>
        </div>-->

        <div class="item">
          <div @click="showeditpharmacyregion()" class="items">
            <div class="itemright">المنطقة</div>
            <div class="itemleft">{{pharmsyInformation.region}}</div>
          </div>

          <div class="edit" ref="editpharmacyregion">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.region"
              ref="pharmacyregioninput"
            />
          </div>
        </div>
        <!-- <div class="item">
          <div class="itemright">الشارع</div>
          <div class="itemleft">{{pharmsyInformation.street}}</div>
        </div>-->

        <div class="item">
          <div @click="showeditpharmacystreet()" class="items">
            <div class="itemright">الشارع</div>
            <div class="itemleft">{{pharmsyInformation.street}}</div>
          </div>

          <div class="edit" ref="editpharmacystreet">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.street"
              ref="pharmacystreetinput"
            />
          </div>
        </div>
        <!-- <div class="item">
          <div class="itemright">رقم المبنى</div>
          <div class="itemleft">{{pharmsyInformation.buildingNumber}}</div>
        </div>-->
        <div class="item">
          <div @click="showeditpharmacybuildingNumber()" class="items">
            <div class="itemright">رقم المبنى</div>
            <div class="itemleft">{{pharmsyInformation.buildingNumber}}</div>
          </div>

          <div class="edit" ref="editpharmacybuildingNumber">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.buildingNumber"
              ref="pharmacybuildingNumberinput"
            />
          </div>
        </div>
        <!-- <div class="item">
          <div class="itemright">اتساع مساحه التوصيل</div>
          <div class="itemleft">{{pharmsyInformation.breadthOfTheConnectionSpace + ' كيلو'}}</div>
        </div>-->
        <div class="item">
          <div @click="showeditpharmacyConnectionSpace()" class="items">
            <div class="itemright">اتساع مساحه التوصيل</div>
            <div class="itemleft">{{pharmsyInformation.breadthOfTheConnectionSpace + ' كيلو'}}</div>
          </div>

          <div class="edit" ref="editpharmacyConnectionSpace">
            <div class="itemright"></div>

            <input
              class="itemleft input is-info asd"
              type="text"
              :value="pharmsyInformation.breadthOfTheConnectionSpace"
              ref="pharmacyConnectionSpaceinput"
            />
          </div>
        </div>
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
const useronerpharmsy =
  "https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information";

export default {
  components: {
    myVav
  },
  data() {
    return {
      pharmsyInformation: [],
      userName: localStorage.getItem("userfirstName")
    };
  },
  methods: {
    async seave() {
      const pharmacyhotlighinput = this.$refs["pharmacyhotlighinput"].value;
      const pharmacycityinput = this.$refs["pharmacycityinput"].value;
      const pharmacyregioninput = this.$refs["pharmacyregioninput"].value;
      const pharmacystreetinput = this.$refs["pharmacystreetinput"].value;
      const pharmacybuildingNumberinput = this.$refs[
        "pharmacybuildingNumberinput"
      ].value;
      const pharmacyConnectionSpaceinput = this.$refs[
        "pharmacyConnectionSpaceinput"
      ].value;

      let id = this.pharmsyInformation.id;
      console.log(id);

      const res = await axios.patch(
        `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/${id}`,
        {
          pharmacyhotligh: pharmacyhotlighinput,
          city: pharmacycityinput,
          region: pharmacyregioninput,
          street: pharmacystreetinput,
          buildingNumber: pharmacybuildingNumberinput,
          breadthOfTheConnectionSpace: pharmacyConnectionSpaceinput
        }
      );
      this.$router.go();
      const edi = await axios.get(useronerpharmsy);
      this.userInformation = edi.data;
    },
    showeditpharmacyhotligh() {
      this.$refs["editpharmacyhotligh"].classList.toggle("edit");
    },
    showeditpharmacycity() {
      this.$refs["editpharmacycity"].classList.toggle("edit");
    },
    showeditpharmacyregion() {
      this.$refs["editpharmacyregion"].classList.toggle("edit");
    },
    showeditpharmacystreet() {
      this.$refs["editpharmacystreet"].classList.toggle("edit");
    },
    showeditpharmacybuildingNumber() {
      this.$refs["editpharmacybuildingNumber"].classList.toggle("edit");
    },
    showeditpharmacyConnectionSpace() {
      this.$refs["editpharmacyConnectionSpace"].classList.toggle("edit");
    }
  },

  async created() {
    const ressearch = await axios.get(
      `https://pharmacy-databeas.herokuapp.com/pharmacyOner-Information/?firstUserName=${this.userName}`
    );
    this.pharmsyInformation = ressearch.data[0];
    console.log(this.pharmsyInformation);
  }
};
</script>

<style scoped>
.asd {
  text-align: left;
}
.edit {
  display: none;
  padding: 20px 0;
}
.items {
  cursor: pointer;
  user-select: none;
}
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