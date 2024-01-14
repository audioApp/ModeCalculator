<template>
  <view class="index">
    <text class="main_message">
      笛子（6孔竹笛）以第三孔的音高定调，比如打开一，二，三孔，吹奏出来的音高是G，那么这就是一支G调笛子
    </text>
  </view>

  <view class="section1">
    <label>笛子的调</label>
    <picker-view
      indicator-style="height: 30px;"
      style="width: 80%; height: 100px; display: inline-block"
      :value="value"
      @change="onChange"
    >
      <picker-view-column>
        <view v-for="(item, index) in years" :key="index">{{ item }}年</view>
      </picker-view-column>
    </picker-view>
  </view>
</template>

<script>
import { ref } from "vue";
import "./index.scss";

export default {
  setup() {
    const msg = ref("Hello ");
    return {
      msg,
    };
  },
  data() {
    const date = new Date();
    const years = [];
    const months = [];
    const days = [];
    for (let i = 1990; i <= date.getFullYear(); i++) {
      years.push(i);
    }
    for (let i = 1; i <= 12; i++) {
      months.push(i);
    }
    for (let i = 1; i <= 31; i++) {
      days.push(i);
    }

    return {
      selector: ["美国", "中国", "巴西", "日本"],
      selectorChecked: "美国",
      timeSel: "12:01",
      dateSel: "2018-04-22",

      years: years,
      year: date.getFullYear(),
      months: months,
      month: 2,
      days: days,
      day: 2,
      value: [3, 1, 1],
    };
  },
  methods: {
    onChange: function (e) {
      this.selectorChecked = this.selector[e.detail.value];
    },
  },
};
</script>
