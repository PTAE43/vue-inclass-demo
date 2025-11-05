<script setup>
import { ref } from "vue";
// 1. ประกาศตัวแปร name มีค่าเริ่มต้นเป็น ""
const name = ref("");

// 2. ประกาศตัวแปร participants เป็น Array เปล่าสำหรับเก็บค่า input name
const participants = ref([]);

// 3. สร้างฟังก์ชันสำหรับเพิ่ม name เข้า participants ตอนที่กดปุ่ม
const addParticipant = () => {
  // เริ่มเขียนโค้ดตรงนี้
  const n = name.value.trim();
  if (!n) return;
  participants.value.push(n);
  name.value = "";
};
</script>

<template>
  <div class="assignment-container">
    <h2>รายชื่อผู้เข้าร่วมกิจกรรม</h2>

    <div class="input-group">
      <!-- 4. ใช้ v-model เพื่อเก็บค่า input -->
      <input v-model="name" placeholder="กรอกชื่อผู้เข้าร่วม" @keyup.enter="addParticipant" />
      <!-- 5. ใช้ @click เพื่อเรียกใช้ addParticipant ตอนกดปุ่ม -->
      <button @click="addParticipant">+ เพิ่มชื่อ</button>
    </div>

    <!-- ย้ายรายการลงมาด้านล่างอินพุต -->
    <div class="participant-list">
      <!-- 6. เขียน v-if เพื่อแสดงข้อความ "ยังไม่มีผู้เข้าร่วม" เมื่อไม่มีสมาชิกใน participants -->
      <p v-if="participants.length === 0">ยังไม่มีผู้เข้าร่วม</p>
      <!-- 7. เขียน v-else เพื่อแสดง <li> ถ้ามีสมาชิกใน participants -->
      <ul v-else>
        <!-- 8. เขียน v-for เพื่อลูปและแสดงรายชื่อทั้งหมดใน participants -->
        <li v-for="(participant, i) in participants" :key="i">
          <span class="badge">{{ i + 1 }}</span>
          <span class="subtext">{{ participant }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.assignment-container {
  max-width: 500px;
  margin: 40px auto;
  padding: 24px;
  border-radius: 12px;
  background: #ffffff;
  text-align: center;
  font-family: "Prompt", sans-serif;
}

h2 {
  color: #333;
  margin-bottom: 20px;
}

.input-group {
  display: flex;
  justify-content: center;
  gap: 8px;
  margin-bottom: 16px;
}

input {
  padding: 5px 14px;
  border-radius: 8px;
  border: 1px solid #ccc;
  outline: none;
  transition: all 0.2s;
  flex: 1;
}

input:focus {
  border-color: #42b883;
}

button {
  background: #42b883;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  padding: 10px 14px;
  transition: background 0.2s;
}

button:hover {
  background: #359f70;
}

.participant-list {
  text-align: left;
  margin-top: 12px;
}

.empty-text {
  text-align: center;
  color: #888;
  margin-top: 10px;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  background: #f4f9f6;
  padding: 8px 12px;
  border-radius: 6px;
  margin-bottom: 6px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.badge {
  background: #42b883;
  color: white;
  font-size: 12px;
  border-radius: 999px;
  min-width: 28px;
  height: 22px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.subtext {
  color: #000000;
}
</style>
