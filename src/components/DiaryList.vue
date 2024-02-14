<template>
  <div class="diarylist">
    <div v-for="(item, ind) in this.data" :key="ind" class="diaryitem">
      <div class="day">
        <h3>{{ item.id }}</h3>
      </div>
      <div class="diaries">
        <div
          v-for="(diary, index) in item.diaryTasks"
          :key="index"
          class="diary"
        >
          <h3 :class="whatcolor(diary.importance)">{{ diary.value }}</h3>
          <div
            class="deleteboxDiary"
            @click.stop="this.$emit('deleteDiary', diary.id)"
          ></div>
        </div>
      </div>
      <div
        class="deleteboxItem"
        @click="this.$emit('deleteByDay', item.id)"
      ></div>
    </div>
  </div>
</template>
<script>
export default {
  props: ["data"],
  emits: ["deleteByDay", "deleteDiary"],
  methods: {
    whatcolor(col) {
      return col === "true" ? "green" : "red";
    },
  },
};
</script>
<style>
h3 {
  font-size: 30px;
  padding-left: 10px;
  color: white;
}
.diarylist {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 83.5vw;
  margin-top: 50px;
}

.diaryitem {
  display: flex;
  align-items: center;
  width: 100%;
  height: fit-content;
  border-radius: 20px;
  background-color: #ecf0f1;
  margin-top: 20px;
  box-sizing: border-box;
}
.day {
  width: 80px;
  background-color: #34495e;
  display: flex;
  border-radius: 20px 0 0 20px;
  align-items: center;
  justify-content: center;
  align-self: stretch;
}
.deleteboxItem {
  opacity: 0;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background-color: #e74c3c;
  border: 1px solid #000000;
  display: flex;
  justify-content: center;
  align-items: center;
  left: 90.5vw;
  align-self: start;
  position: absolute;
}
.deleteboxItem::after {
  content: "";
  position: absolute;
  transform: rotate(45deg);
  width: 18px;
  height: 2px;
  background-color: #000000;
}
.deleteboxItem::before {
  content: "";
  position: absolute;
  transform: rotate(-45deg);
  width: 18px;
  height: 2px;
  background-color: #000000;
}
.green {
  background-color: green;
  padding: 0 0 0 0;
  margin: 0;
}
.red {
  background-color: red;
  padding: 0 0 0 0;
  margin: 0;
}
.diaries {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  width: 75vw;
  gap: 15px;
  padding: 10px;
  height: fit-content;
}
.diary {
  width: 286px;
  height: fit-content;
  margin-left: 30px;
  position: relative;
}
.diary > h3 {
  padding: 2px 5px 5px 15px;
  font-weight: 400;
}
.deleteboxDiary {
  opacity: 0;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background-color: #e74c3c;
  border: 1px solid #000000;
  display: flex;
  justify-content: center;
  align-items: center;
  bottom: 25px;
  left: 270px;
  position: absolute;
}
.deleteboxDiary::after {
  content: "";
  position: absolute;
  transform: rotate(45deg);
  width: 18px;
  height: 2px;
  background-color: #000000;
}
.deleteboxDiary::before {
  content: "";
  position: absolute;
  transform: rotate(-45deg);
  width: 18px;
  height: 2px;
  background-color: #000000;
}
.diaryitem:hover .deleteboxItem {
  transition: 0.3s;
  opacity: 100;
}
.diary:hover .deleteboxDiary {
  transition: 0.3s;
  opacity: 100;
}
</style>
