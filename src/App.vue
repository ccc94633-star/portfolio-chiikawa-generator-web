<script setup>

import { ref } from 'vue'
import defaultImg from '@/assets/images/default.webp'
import weaponImg from '@/assets/images/weapon.jpg'

const memberName = ref('');
const memberAge = ref('');
const memberLevel = ref('');
const memberImg = ref('');
const detail = ref('');
const memberVip = ref('');
const levelNames = {
  cute: '努力的小可愛',
  stressed: '追求強大的小可愛',
  chimera: '距離變身為奇美拉已經不遠的小可愛',
}
const levelLabels = {
  cute: '又小又可愛的吉伊卡哇',   // 顯示等級用
  stressed: '壓力山大的吉伊卡哇',
  chimera: '即將黑化的奇美拉',
}

</script>



<template>
  <h1>吉伊卡哇樂園島民產生器</h1>
  <div id="app">

    <section class="input-card">
      <span>吉伊卡哇樂園申請入島表單</span>
      <label for="name">
        <div>姓名:
          <input type="text" id="name" v-model="memberName" placeholder="請輸入姓名">
        </div>
      </label>
      <label for="age">
        <div>年齡:
          <input type="number" id="age" v-model="memberAge" placeholder="請輸入年齡">
        </div>
      </label>
      <label for="level">
        <div>黑化等級:
          <select id="level" v-model="memberLevel">
            <option value="" hidden>請選擇</option>
            <option value="cute">努力的小可愛</option>
            <option value="stressed">追求強大的小可愛</option>
            <option value="chimera">即將黑化的奇美拉</option>
          </select>
        </div>
      </label>
      <label for="img">
        <div>頭像圖片網址:
          <input type="url" id="memberImg" v-model="memberImg" placeholder="請上傳您的頭像圖片網址">
        </div>
      </label>
      <label for="detail">
        <div>顯示島民資料:
          <input type="checkbox" id="detail" v-model="detail">
        </div>
      </label>
      <label for="vip">
        <div>啟動討閥模式:
          <input type="checkbox" id="vip" v-model="memberVip">
        </div>
      </label>

    </section>



    <!-- 如果輸入姓名 才顯示整張小卡 -->
    <!-- memberName不是null時，才將class覆蓋output-card -->


    <!-- { vip: memberVip } — 物件格式：{ class名稱: 條件 } -->
    <!-- memberVip = true // → <div class="vip">
            memberVip = false // → <div class=""> -->

    <section v-if="memberName.trim()" class="output-card" :class="{ vip: memberVip }">
      <span>吉伊卡哇入島申請預覽</span>

      <!-- 頭像 -->
      <div>
        <img class="avatar" v-if="memberImg" :src="memberImg" :alt="memberName + '的頭像'">
        <img class="avatar" v-else :src="defaultImg" :alt="memberName + '的頭像'">
      </div>

      <!-- 姓名 -->
      <div class="member-name">{{ memberName }}</div>

      <hr>

      <!-- 年齡 -->
      <div class="member-age">{{ memberAge }}歲</div>

      <!-- 等級 -->
      <div class="member-level">{{ levelNames[memberLevel] }}</div>

      <hr>

      <!-- 詳細資料 -->
      <div class="member-detail" v-show="detail">這是一位{{ levelNames[memberLevel] }}，
        <br>
        歡迎加入這個充滿美食與危險的小島！
      </div>
      <!-- VIP -->
      <div class="vip-section" v-show="memberVip">
        <img :src="weaponImg" :alt="memberName+'拿起武器'">
        <div class="vip-text">★ 拿起討閥棒，向前衝啊！ ★</div>
      </div>

    </section>



  </div>

</template>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: linear-gradient(135deg, #FFF8E7 0%, #FFE4EF 55%, #E8F4FF 100%);
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-content: center;
  min-height: 100vh;
  padding: 36px 20px;
}



#app {
  display: flex;
  justify-content: center;
  font-family: '微軟正黑體';
  gap: 30px;
  border-radius: 10px;
  flex-wrap: wrap;
}


section.input-card {
  background-color: lightpink;
  display: flex;
  flex-direction: column;
  align-items: start;
  gap: 10px;
  padding: 30px 34px;
  box-shadow: 0 8px 32px rgba(255, 143, 163, 0.18);
  border-radius: 28px;
}


section.output-card {

  background-color: lightyellow;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  border-radius: 28px;
  padding: 30px 34px;
  border: 2.5px solid #FFD6E0;
  box-shadow: 0 8px 32px rgba(255, 143, 163, 0.18);
}

h1 {
  text-align: center;
  color: #FF8FA3;
  font-size: 1.9rem;
  font-weight: 700;
  margin-bottom: 36px;
  letter-spacing: 3px;
  text-shadow: 2px 3px 0px #FFD6E0;
}


span {
  color: #e11b64;
  font-size: 1rem;
  text-align: center;
  padding-bottom: 12px;
  border-bottom: 2px dashed #FFD6E0;
  letter-spacing: 1px;
}


img {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border-radius: 50%;
}

#arms {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input[type="checkbox"] {
  width: 18px;
  height: 18px;
  accent-color: #FF8FA3;
  cursor: pointer;
}




/* 討閥模式　　ＶＩＰ */
section.output-card.vip {
  background: linear-gradient(160deg, #FFFCEB, #FFF3C4);
  border-color: #F5C518;
  box-shadow: 0 8px 32px rgba(245, 197, 24, 0.35), 0 0 24px rgba(245, 197, 24, 0.15);
}

section.output-card.vip h2 {
  color: #C8960C;
  border-bottom-color: #F5C518;
}

/* 頭像 */
img.avatar {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border-radius: 50%;
  border: 4px solid #FFD6E0;
  box-shadow: 0 4px 14px rgba(255, 143, 163, 0.28);
}

.vip img.avatar {
  border-color: #F5C518;
  box-shadow: 0 4px 14px rgba(245, 197, 24, 0.4);
}

/* 姓名 */
.member-name {
  font-size: 1.35rem;
  font-weight: 700;
  color: #FF8FA3;
  letter-spacing: 2px;
}

.vip .member-name {
  color: #C8960C;
}

/* 年齡 */
.member-age {
  font-size: 0.88rem;
  color: #BBA0A8;
}

/* 等級 */
.member-level {
  background: #FFE8F0;
  color: #FF8FA3;
  padding: 5px 20px;
  border-radius: 50px;
  font-size: 0.82rem;
  font-weight: 700;
  letter-spacing: 0.5px;
  border: 1.5px solid #FFD6E0;
}

.vip .member-level {
  background: #FFF0B8;
  color: #C8960C;
  border-color: #F5C518;
}

hr {
  width: 75%;
  border: none;
  border-top: 2px dashed #FFD6E0;
}

.vip hr {
  border-top-color: #F5C518;
}

/* 詳細資料 */
.member-detail {
  background: #FFF6FA;
  border-radius: 16px;
  padding: 12px 16px;
  font-size: 0.84rem;
  color: #A08090;
  line-height: 1.9;
  border: 1.5px dashed #FFD6E0;
  width: 100%;
}

.vip .member-detail {
  background: #FFFBEC;
  border-color: #F5C518;
  color: #9A7020;
}

/* VIP 討閥區 */
.vip-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.vip-section img {
  width: 90px;
  height: 90px;
  object-fit: cover;
  border-radius: 50%;
  border: 4px solid #F5C518;
  box-shadow: 0 4px 14px rgba(245, 197, 24, 0.4);
}

.vip-text {
  color: #C8960C;
  font-weight: 700;
  font-size: 0.9rem;
  letter-spacing: 1px;
  background: #FFF0B8;
  padding: 5px 18px;
  border-radius: 50px;
  border: 1.5px solid #F5C518;
}
</style>
