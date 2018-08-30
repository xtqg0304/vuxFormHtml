<template>
  <div class="appointmentBox">
    <flexbox orient="vertical">
      <flexbox-item>
        <p class="appointmentBoxTitle">请填写您的信息</p>
        <group>
          <x-input title="您的姓名" type="" placeholder="必填" required></x-input>
          <x-input mask="999 9999 9999" v-model="data.phone" title="手机号码" name="mobile" placeholder="请输入手机号码" keyboard="number" is-type="china-mobile"></x-input>
          <x-input title="身份证" name="IDcard" placeholder="请输入身份证" keyboard="number" @on-blur="isIDcard" required></x-input>
          <x-textarea :max="20" placeholder="请输入您的单位"></x-textarea>
        </group>

      </flexbox-item>
      <flexbox-item>
        <x-button type="primary">primary</x-button>
      </flexbox-item>
      <flexbox-item>
        <p class="appointmentBoxTitle">请填写预约信息</p>
        <group>
          <datetime v-if="noonValue" title="访问时间" ref="datetime" :start-date="today" v-model="noonValue" format="YYYY-MM-DD A" @on-change="change" required placeholder="请选择"></datetime>
          <!-- <x-input title="访问时间" type="" placeholder="必填"></x-input> -->
          <x-input mask="999 9999 9999" v-model="data.phone" title="手机号码" name="mobile" placeholder="请输入手机号码" keyboard="number" is-type="china-mobile"></x-input>
          <x-number :value="10" title="到访人数" fillable></x-number>
          <popup-radio title="到访事由" :options="list1" v-model="value1" placeholder="请选择"></popup-radio>
          <x-input title="请输入车牌号" type="" placeholder="必填" @on-focus="onFocus" @on-blur="onBlur" required></x-input>
        </group>

      </flexbox-item>
    </flexbox>
    <flexbox>
      <flexbox-item>
        <x-button type="primary">我的信息</x-button>
      </flexbox-item>
      <flexbox-item>
        <x-button type="primary">预约</x-button>
      </flexbox-item>

    </flexbox>
    <flexbox>
      <flexbox-item>
        <cell title="详细信息"></cell>
        <cell-form-preview :list="list"></cell-form-preview>
        <divider>{{ "您的凭证" }}</divider>
        <qrcode style="text-align:center" value="https://vux.li?x-page=demo_qrcode" type="img"></qrcode>
      </flexbox-item>

    </flexbox>
    <flexbox orient="vertical">
      <flexbox-item>
        <p class="appointmentBoxTitle">请先绑定员工信息</p>
        <group>
          <x-input mask="999 9999 9999" v-model="data.phone" title="手机号码" name="mobile" placeholder="请输入手机号码" keyboard="number" is-type="china-mobile"></x-input>
          <x-input title="验证码" class="weui-vcode" required>
            <x-button slot="right" type="primary" mini>发送验证码</x-button>
          </x-input>
        </group>

      </flexbox-item>
      <flexbox-item>
        <x-button type="primary">提交</x-button>
      </flexbox-item>
    </flexbox>
    <flexbox orient="vertical">
      <flexbox-item>
        <p class="appointmentBoxTitle">请先填写邀请信息</p>
        <group>
          <x-input title="贵宾姓名" type="" placeholder="必填" required></x-input>
          <x-input mask="999 9999 9999" v-model="data.phone" title="贵宾手机" name="mobile" placeholder="请输入手机号码" keyboard="number" is-type="china-mobile"></x-input>
          <datetime v-if="noonValue" title="来访时间" ref="datetime" :start-date="today" v-model="noonValue" format="YYYY-MM-DD A" @on-change="change" required placeholder="请选择"></datetime>
        </group>

      </flexbox-item>
      <flexbox-item>
        <x-button type="primary">提交</x-button>
      </flexbox-item>
    </flexbox>
  </div>
</template>

<script>
import { Flexbox, FlexboxItem, Group, Cell, XInput, XTextarea, XButton, XNumber, PopupRadio, CellFormPreview, Qrcode, Divider, Datetime } from 'vux'
export default {
  name: '',
  components: {
    Flexbox,
    FlexboxItem,
    Group,
    Cell,
    XInput,
    XTextarea,
    XButton,
    XNumber,
    PopupRadio,
    CellFormPreview,
    Qrcode,
    Divider,
    Datetime
  },
  data() {
    return {
      msg: '',
      data: {
        name: '',
        phone: '',
        IDcard: '',
        company: ''
      },
      list1: ['预约参观', '邀请访问'],
      value1: '预约参观',
      list: [{
        label: '访问类型',
        value: '访客预约'
      }, {
        label: '访客姓名',
        value: '小豪'
      }, {
        label: '访客手机',
        value: '12574585522'
      }, {
        label: '员工姓名',
        value: '唐经理'
      }, {
        label: '员工手机',
        value: '12574585522'
      }, {
        label: '来访人数',
        value: '125'
      }, {
        label: '邀访事由',
        value: '预约参观'
      }, {
        label: '车牌号',
        value: '闽A1254'
      }, {
        label: '见面地址',
        value: '星网锐捷海西科技园'
      }],
      noonValue: '2018-08-25 PM',
      today: ''

    }
  },
  methods: {
    isVehicleNo(str) {
      return /^(([\u4E00-\u9FA5][A-Z](([0-9]{5}[DF])|([DF]([A-HJ-NP-Z0-9])[0-9]{4})))|([\u4E00-\u9FA5][A-Z][A-HJ-NP-Z0-9]{4}[A-HJ-NP-Z0-9挂学警港澳使领]))$/.test(str);
    },
    onFocus(val) {
      // console.log(val)
    },
    onBlur(val) {
      console.log(val)
      console.log(this.isVehicleNo(val))
      console.log(!this.isVehicleNo(val))
      if (val) {
        if (!this.isVehicleNo(val) == true) {
          event.target.parentNode.parentNode.classList.add("weui-cell_warn")
        } else {
          if (event.target.parentNode.parentNode.classList.contains("weui-cell_warn")) {
            event.target.parentNode.parentNode.classList.remove("weui-cell_warn")
          }

        }
      }

    },
    setToday() {
      let now = new Date()
      let cmonth = now.getMonth() + 1
      let day = now.getDate()
      let hour = now.getHours()
      if (cmonth < 10) cmonth = '0' + cmonth
      if (day < 10) day = '0' + day
      this.today = now.getFullYear() + '-' + cmonth + '-' + day;

    },
    change(value) {
      this.noonValue = value
      this.$refs.datetime.render()
      console.log('this.noonValue', this.noonValue)
    },
    isIDcard(val) {
      if (val) {
        if (!this.IdentityCodeValid(val) == true) {
          event.target.parentNode.parentNode.classList.add("weui-cell_warn")
        } else {
          if (event.target.parentNode.parentNode.classList.contains("weui-cell_warn")) {
            event.target.parentNode.parentNode.classList.remove("weui-cell_warn")
          }

        }
      }
    }
    ,
    IdentityCodeValid(code) {
      var city = { 11: "北京", 12: "天津", 13: "河北", 14: "山西", 15: "内蒙古", 21: "辽宁", 22: "吉林", 23: "黑龙江 ", 31: "上海", 32: "江苏", 33: "浙江", 34: "安徽", 35: "福建", 36: "江西", 37: "山东", 41: "河南", 42: "湖北 ", 43: "湖南", 44: "广东", 45: "广西", 46: "海南", 50: "重庆", 51: "四川", 52: "贵州", 53: "云南", 54: "西藏 ", 61: "陕西", 62: "甘肃", 63: "青海", 64: "宁夏", 65: "新疆", 71: "台湾", 81: "香港", 82: "澳门", 91: "国外 " };
      var tip = "";
      var pass = true;

      if (!code || !/^\d{6}(18|19|20)?\d{2}(0[1-9]|1[012])(0[1-9]|[12]\d|3[01])\d{3}(\d|X)$/i.test(code)) {
        tip = "身份证号格式错误";
        pass = false;
      }

      else if (!city[code.substr(0, 2)]) {
        tip = "地址编码错误";
        pass = false;
      }
      else {
        //18位身份证需要验证最后一位校验位
        if (code.length == 18) {
          code = code.split('');
          //∑(ai×Wi)(mod 11)
          //加权因子
          var factor = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2];
          //校验位
          var parity = [1, 0, 'X', 9, 8, 7, 6, 5, 4, 3, 2];
          var sum = 0;
          var ai = 0;
          var wi = 0;
          for (var i = 0; i < 17; i++) {
            ai = code[i];
            wi = factor[i];
            sum += ai * wi;
          }
          var last = parity[sum % 11];
          if (parity[sum % 11] != code[17]) {
            tip = "校验位错误";
            pass = false;
          }
        }
      }
      if (!pass) alert(tip);
      return pass;
    },
    setStyle() {
      console.log(previewbd)
      let previewbd = document.getElementsByClassName("weui-form-preview__bd")[0];
      previewbd.style.textAlign = "left";
      previewbd.style.fontSize = "inherit";
      previewbd.style.color = "inherit";
    }
  },
  created() {
    this.setToday()

  },
  mounted() {
    this.setStyle()
  }
}
</script>

<style scoped>
.appointmentBox {
  margin: 20px;
  text-align: center;
}
.appointmentBoxTitle {
  background: #def1df;
  padding: 12px 0;
  font-size: 1.6rem;
  color: #3c863b;
  text-align: center;
}
</style>
