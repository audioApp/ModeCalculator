<template>
  <div class="container">
    <text class="main_message">
      笛子（6孔竹笛）以第三孔的音高定调，比如打开一，二，三孔，吹奏出来的音高是G，那么这就是一支G调笛子
    </text>

    <div class="section">
      <text class="section_text">笛子的调</text>
      <el-select size="small" style="width: 80px" v-model="currentModelOfDizi">
        <el-option v-for="item in modelOfDizi" :key="item" :label="textOf(item)" :value="item" />
      </el-select>
    </div>
    <div class="section">
      <text class="section_text">筒音的调</text>
      <text class="section_detial">{{ textOf(lowKey) }}调</text>
    </div>

    <div class="section">
      <text class="section_text">筒音当作</text>
      <el-select size="small" style="width: 80px" v-model="currentFingerStyle">
        <el-option v-for="(item, index) in fingerStyles" :key="index" :label="item" :value="item" />
      </el-select>
    </div>
    <view class="section">
      <text class="section_text">曲子的调</text>
      <text class="section_detial">{{ textOf(musicKey) }}调</text>
    </view>
  </div>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'

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
  B
}

function textOf(type: MusicalAlphabet) {
  switch (type) {
    case MusicalAlphabet.C:
      return 'C'
    case MusicalAlphabet.bD:
      return 'bD'
    case MusicalAlphabet.D:
      return 'D'
    case MusicalAlphabet.bE:
      return 'bE'
    case MusicalAlphabet.E:
      return 'E'
    case MusicalAlphabet.F:
      return 'F'
    case MusicalAlphabet.bG:
      return 'bG'
    case MusicalAlphabet.G:
      return 'G'
    case MusicalAlphabet.bA:
      return 'bA'
    case MusicalAlphabet.A:
      return 'A'
    case MusicalAlphabet.bB:
      return 'bB'
    case MusicalAlphabet.B:
      return 'B'
  }
}

const modelOfDizi = [
  MusicalAlphabet.bB,
  MusicalAlphabet.C,
  MusicalAlphabet.D,
  MusicalAlphabet.E,
  MusicalAlphabet.F,
  MusicalAlphabet.G,
  MusicalAlphabet.A
]

const fingerStyles = [1, 2, 3, 4, 5, 6, 7]
const semitone: any = { 1: 0, 2: 2, 3: 4, 4: 5, 5: 7, 6: 9, 7: 11, 8: 12 }
const currentModelOfDizi = ref(MusicalAlphabet.C)
const currentFingerStyle = ref(1)

const lowKey = computed(() => {
  let r = (currentModelOfDizi.value - 5 + 12) % 12
  console.log(`lowkey reuslt :${r}`)
  return r
})

const musicKey = computed(() => {
  let r = (currentModelOfDizi.value - 5 - semitone[currentFingerStyle.value] + 24) % 12
  console.log(`musicKey reuslt :${r}`)
  return r
})
</script>

<style scoped>
.main_message {
  color: teal;
}

.container {
  display: flex;
  flex-direction: column;
}

.section {
  display: flex;
  align-items: center;
  margin-top: 10pt;
  margin-left: 8pt;
  margin-right: 8pt;
}

.section_text {
  margin-left: 20pt;
  width: 25%;
}

.section_detial {
  width: 60%;
  background-color: tan;
  text-align: center;
}
</style>
