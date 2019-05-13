<template>
  <div class="model_addr" v-show="addr.isShow">
    <div class="model-bg" @click="saveAddrClick"></div>
    <div class="model-body">
      <div class="model-header c_flex c_flex_between c_item_center">
        <div class="model-title">城市地区选择</div>
        <div class="model-cancel" @click="saveAddrClick(true)">×</div>
      </div>
      <div class="model-hot">
        <div class="model-hot-title">热门省市</div>
        <div class="model-hot-list c_flex">
          <div class="model-hot-group" v-for="(item,index) in addr.hotList" :key="index"
               :class="((addr.province==item.province)&&(addr.city==item.city))?'bg_red':''">
            <div class="model-item c_flex c_flex_center" @click="hotClick(item)">
              {{item.name}}
            </div>
          </div>
        </div>
      </div>
      <div class="model-choose">
        <div class="model-hot-title">省市区选择</div>
        <div class="model-choose-title c_flex">
          <div :class="addr.province?'':'c_red'" @click="chooseAddress('province')">{{addr.province||'请选择'}}</div>
          <div v-show="addr.province" :class="addr.city?'':'c_red'" @click="chooseAddress('city')">
            {{addr.city||'请选择'}}
          </div>
          <div v-show="addr.province && addr.city" :class="addr.district?'':'c_red'" @click="chooseAddress('district')">
            {{addr.district||'请选择'}}
          </div>
        </div>
        <div class="model-choose-list">
          <div class="model-choose-group" :class="index % 2 ==0 ? 'bg-fcfcfc':'bg_white' "
               v-for="(item,index) in addr.chooseList" :key="index">
            <div class="model-item"
                 :class="addr.chooseType=='province'?(item.name==addr.province?'c_red':''):(addr.chooseType=='city'?(item.name==addr.city?'c_red':''):(addr.district==item.name?'c_red':''))"
                 @click="chooseClick(item)">
              {{item.name}}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  // <c-area @saveAddrClick="saveAddrClick" :addrtemp="addr" :province="province" :city="city" :district="district"></c-area>
  var addressList = require('../comm/addressList.js');
  export default {
    name: "c-area",
    data() {
      return {
        // province: '',
        // city: '',
        // district: '',
        addr: {
          chooseType: 'province',
          province: '',
          city: '',
          district: '',
          hotList: [
            {name: '北京', type: 'district', province: '北京市', city: '北京市', district: ''},
            {name: '天津', type: 'district', province: '天津市', city: '天津市', district: ''},
            {name: '四川', type: 'city', province: '四川省', city: '', district: ''},
            {name: '陕西', type: 'city', province: '陕西省', city: '', district: ''},
            {name: '武汉', type: 'district', province: '湖北省', city: '武汉市', district: ''},
            {name: '上海', type: 'district', province: '上海市', city: '上海市', district: ''},
            {name: '杭州', type: 'district', province: '浙江省', city: '杭州市', district: ''},
            {name: '广州', type: 'district', province: '广东省', city: '广州市', district: ''},
          ],
          chooseList: [],
          provinceList: [],
          cityList: [],
          districtList: [],
          isShow: false,
        },
      }
    },
    props: {
      province:String,
      city:String,
      district:String,
      addrtemp:Object,
    },
    mounted() {
      this.province = this.province;
      this.city = this.city;
      this.district = this.district;
      this.addr = this.addrtemp;
      this.getProvinceList();
    },
    methods: {
      getProvinceList: function () {
        let addr = addressList.default.addressData;
        this.addr.province = this.province||'';
        this.addr.city = this.city||'';
        this.addr.district = this.district||'';
        this.addr.provinceList = addr;
        if(this.province){
          this.chooseAddress('district');
        }else{
          this.chooseAddress('province');
        }
      },
      chooseAddress: function (type) {
        if (type == 'province') {
          this.addr.chooseList = this.addr.provinceList;
          this.addr.province = '';
          this.addr.city = '';
          this.addr.district = '';
          this.addr.cityList = [];
          this.addr.districtList = [];
        } else if (type == 'city' && this.addr.province) {
          var provinceList = this.addr.provinceList;
          var cityList = [];
          for (let i = 0, j = provinceList.length; i < j; i++) {
            if (provinceList[i].name == this.addr.province) {
              cityList = provinceList[i].child;
              break;
            }
          }
          this.addr.cityList = cityList;
          this.addr.city = '';
          this.addr.district = '';
          this.addr.districtList = [];
          this.addr.chooseList = cityList;
        } else if (type == 'district' && this.addr.province && this.addr.city) {
          var cityList = this.addr.cityList || [];
          if (cityList.length < 1) {
            var provinceList = this.addr.provinceList;
            for (let i = 0, j = provinceList.length; i < j; i++) {
              if (provinceList[i].name == this.addr.province) {
                cityList = provinceList[i].child;
                break;
              }
            }
          }
          var districtList = [];
          for (let ii = 0, jj = cityList.length; ii < jj; ii++) {
            if (cityList[ii].name == this.addr.city) {
              districtList = cityList[ii].child;
              break;
            }
          }
          if(!this.addr.district){ this.addr.district = '';}
          this.addr.districtList = districtList;
          this.addr.chooseList = districtList;
        }
        this.addr.chooseType = type;
      },
      chooseClick: function (item) {
        var chooseType = this.addr.chooseType;
        if (chooseType == 'province') {
          this.addr.province = item.name;
          this.addr.cityList = item.child;
          this.addr.chooseList = item.child;
          this.addr.chooseType = 'city';
        } else if (chooseType == 'city') {
          this.addr.city = item.name;
          this.addr.districtList = item.child;
          this.addr.chooseList = item.child;
          this.addr.chooseType = 'district';
        } else if (chooseType == 'district') {
          this.addr.district = item.name;
          this.saveAddrClick();
        }
      },
      hotClick: function (item) {
        this.addr.province = item.province;
        this.addr.city = item.city;
        this.addr.district = item.district;
        this.addr.cityList = [];
        this.addr.districtList = [];
        this.addr.chooseType = item.type;
        this.chooseAddress(item.type);
      },
      saveAddrClick: function (bool) {
        if (!bool) {
          this.province = this.addr.province;
          this.city = this.addr.city;
          this.district = this.addr.district;
          this.$emit('saveAddrClick',this.addr);
        }
        this.addr.isShow = false;
      },
    },
    watch:{
      "addr.isShow":function (val) {
        if(val){
          this.getProvinceList();
        }
      }
    }
  }
</script>

<style scoped>
  /*.model_addr*/
  .model_addr {
    position: fixed;
    bottom: 0;
    left: 0;
    z-index: 22;
    width: 100vw;
    height: 100vh;
  }

  .model-bg {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, .5);
    z-index: 25;
  }

  .model_addr .model-body {
    position: absolute;
    bottom: 0;
    left: 0;
    z-index: 30;
    width: 100%;
    height: 65vh;
    background: #fff;
  }

  .model_addr .model-header {
    height: 6vh;
    padding: 0 5vw;
    border-bottom: .5px solid #ccc;
    font-size: 15px;
  }

  .model_addr .model-hot-title {
    font-size: 12px;
    color: #878787;
    padding: 3vw;
  }

  .model_addr .model-hot-list {
    padding: 0 5vw;
    width: 100%;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    font-size: 14px;
    flex-wrap: wrap;
  }

  .model_addr .model-hot-group.bg_red {
    color: #fff;
    background: #dc1f31;
  }

  .model_addr .model-hot-group {
    padding: 2vw 5vw;
    background: #f2f2f2;
    border-radius: 5vw;
    margin-bottom: 2vw;
    margin-right: 3vw;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    flex-wrap: wrap;
  }

  .model_addr .model-choose-title {
    border-bottom: .5px solid #f2f2f2;
    box-sizing: border-box;
    width: 100%;
    padding: 0 5vw;
    font-size: 14px;
  }

  .model_addr .model-choose-title div.c_red {
    border-bottom: 1px solid #dc1f31;
    margin-bottom: 1px;
  }

  .model_addr .model-choose-title div {
    height: 8vw;
    max-width: 30vw;
    margin-right: 15px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  .model_addr .model-body,
  .model_addr .model-choose {
    display: flex;
    flex-direction: column;
  }

  .model_addr .model-choose {
    flex: 1;
    overflow: auto;
  }

  .model_addr .model-choose-list {
    width: 100%;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    /*height: calc( 100% - 30vh);*/
    /*height: 38vh;*/
    flex: 1;
    overflow-x: hidden;
    overflow-y: auto;
  }

  .model_addr .model-choose-group {
    padding: 3vw 5vw;
    text-align: left;
  }

  .bg-fcfcfc {
    background: #fcfcfc;
  }
</style>
