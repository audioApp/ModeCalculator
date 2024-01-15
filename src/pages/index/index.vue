<template>
  <view class="index">
    <text class="main_message">
      笛子（6孔竹笛）以第三孔的音高定调，比如打开一，二，三孔，吹奏出来的音高是G，那么这就是一支G调笛子
    </text>
  </view>

  <view class="section">
    <text class="section_text">笛子的调</text>
    <picker-view
      indicator-style="height: 30px;"
      style="width: 60%; height: 100px; display: inline-block"
      @change="onChangeModelOfDizi"
    >
      <picker-view-column>
        <view v-for="(item, index) in modelOfDizi" :key="index"
          >{{ textOf(item) }}调</view
        >
      </picker-view-column>
    </picker-view>
  </view>
  <view class="section">
    <text class="section_text">筒音的调</text>
    <text class="section_detial">{{ textOf(lowKey) }}调</text>
  </view>

  <view class="section">
    <text class="section_text">筒音当作</text>
    <picker-view
      indicator-style="height: 30px;"
      style="width: 60%; height: 100px; display: inline-block"
      @change="onChangeStyle"
    >
      <picker-view-column>
        <view v-for="(item, index) in fingerStyles" :key="index">{{
          item
        }}</view>
      </picker-view-column>
    </picker-view>
  </view>
  <view class="section">
    <text class="section_text">曲子的调</text>
    <text class="section_detial">{{ textOf(musicKey) }}调</text>
  </view>
</template>

<script setup lang="ts">
import { computed, ref, watch } from "vue";
import "./index.scss";

enum MusicalAlphabet {
  C = 0,
  bD,
  D,
  bE,
  E,
  F,
  bG,
  G,
  bA,
  A,
  bB,
  B,
}

function textOf(type: MusicalAlphabet) {
  switch (type) {
    case MusicalAlphabet.C:
      return "C";
    case MusicalAlphabet.bD:
      return "bD";
    case MusicalAlphabet.D:
      return "D";
    case MusicalAlphabet.bE:
      return "bE";
    case MusicalAlphabet.E:
      return "E";
    case MusicalAlphabet.F:
      return "F";
    case MusicalAlphabet.bG:
      return "bG";
    case MusicalAlphabet.G:
      return "G";
    case MusicalAlphabet.bA:
      return "bA";
    case MusicalAlphabet.A:
      return "A";
    case MusicalAlphabet.bB:
      return "bB";
    case MusicalAlphabet.B:
      return "B";
  }
}

const modelOfDizi = [
  MusicalAlphabet.bB,
  MusicalAlphabet.C,
  MusicalAlphabet.D,
  MusicalAlphabet.E,
  MusicalAlphabet.F,
  MusicalAlphabet.G,
  MusicalAlphabet.A,
];

const fingerStyles = [1, 2, 3, 4, 5, 6, 7];
const semitone = { 1: 0, 2: 2, 3: 4, 4: 5, 5: 7, 6: 9, 7: 11, 8: 12 };
const currentModelOfDizi = ref(MusicalAlphabet.C);
const currentFingerStyle = ref(0);

const onChangeModelOfDizi = (e) => {
  const index = e.detail.value[0];
  const val = modelOfDizi[index];
  console.log(`model of dizi ${val}`);
  currentModelOfDizi.value = val;
};

const lowKey = computed(() => {
  let r = (currentModelOfDizi.value - 5 + 12) % 12;
  console.log(`lowkey reuslt :${r}`);
  return r;
});

const onChangeStyle = (e) => {
  const val = e.detail.value[0] + 1;
  const c = semitone[val];
  currentFingerStyle.value = c;
  console.log(`style index:${c}`);
  console.log(c);
};

const musicKey = computed(() => {
  let r = (currentModelOfDizi.value - 5 - currentFingerStyle.value + 24) % 12;
  console.log(`musicKey reuslt :${r}`);
  return r;
});
</script>
