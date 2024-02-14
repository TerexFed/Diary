<template>
  <div class="container">
    <Form @submit="submit" :data="diaryList"></Form>
    <diary-list
      @deleteByDay="deleteByDay"
      @deleteDiary="deleteDiary"
      :data="sortedDiaryList"
    ></diary-list>
  </div>
</template>
<script>
import DiaryList from "./components/DiaryList.vue";
import Form from "./components/Form.vue";

export default {
  components: { Form, DiaryList },
  data() {
    return {
      diaryList: [],
    };
  },
  methods: {
    submit(dayID, imp, val) {
      for (let i = 0; i < this.diaryList.length; i++) {
        if (this.diaryList[i].id === dayID) {
          this.diaryList[i].diaryTasks.push({
            id: Date.now(),
            importance: imp,
            value: val,
          });
          return "";
        }
      }
      this.diaryList.push({
        id: dayID,
        diaryTasks: [
          {
            id: Date.now(),
            importance: imp,
            value: val,
          },
        ],
      });
      console.log(this.diaryList);
    },
    deleteByDay(day) {
      this.diaryList = this.diaryList.filter((el) => el.id !== day);
    },
    deleteDiary(diaryId) {
      for (let i = 0; i < this.diaryList.length; i++) {
        this.diaryList[i].diaryTasks = this.diaryList[i].diaryTasks.filter(
          (el) => el.id !== diaryId
        );

        if (this.diaryList[i].diaryTasks.length === 0) {
          this.diaryList = this.diaryList.filter(
            (el) => el.id !== this.diaryList[i].id
          );
        }
      }
    },
  },
  computed: {
    sortedDiaryList() {
      const dayOrder = ["ПН", "ВТ", "СР", "ЧТ", "ПТ", "СБ", "ВС"];

      return this.diaryList.slice().sort((a, b) => {
        const indexA = dayOrder.indexOf(a.id);
        const indexB = dayOrder.indexOf(b.id);

        return indexA - indexB;
      });
    },
  },
};
</script>
<style>
body {
  font-family: "Inter", sans-serif;
  font-weight: 400;
  margin: 0;
  padding: 0;
  background-color: #1abc9c;
  display: flex;
  justify-content: center;
}
p {
  font-size: 20px;
  color: black;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 80vw;
}
</style>
