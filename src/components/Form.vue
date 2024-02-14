<template>
  <form v-on:click="prevent($event)">
    <div class="options">
      <div class="option">
        <select name="day" v-model="day" >
          <option disabled value="">Выберите день</option>
          <option value="ПН">Понедельник</option>
          <option value="ВТ">Вторник</option>
          <option value="СР">Среда</option>
          <option value="ЧТ">Четверг</option>
          <option value="ПТ">Пятница</option>
          <option value="СБ">Суббота</option>
          <option value="ВС">Воскресенье</option>
        </select>
        <select name="importance" v-model="importance">
          <option disabled value="">Выберите важность</option>
          <option value="true">Важно</option>
          <option value="false">Не важно</option>
        </select>
      </div>
      <input type="text" placeholder="Описание" v-model="inputVal" />
    </div>
    <button @click="this.day !== '' && this.importance !== '' && this.inputVal !== '' ? this.$emit('submit', this.day, this.importance, this.inputVal) : ''">Добавить</button>
  </form>
</template>
<script>
export default {
  emits: ['submit'],
  data() {
    return {
      day: "",
      importance: "",
      inputVal: "",
    };
  },
  methods: {
    prevent(e) {
      e.preventDefault();
    },
    
  },
};
</script>
<style>
form {
  background-color: #ecf0f1;
  border: 1px solid black;
  border-radius: 20px;
  width: 80vw;
  padding: 30px 30px 10px 30px;
  margin-top: 100px;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}
.options {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr 2fr;
  align-items: center;
  gap: 20px;
}
.option {
  display: flex;
  align-items: center;
  width: fit-content;
  height: 45px;
}

.option > select {
  width: 250px;
  height: 45px;
  border-radius: 0px;
  border: 1px solid black;
  font-size: 20px;
  position: relative;
}
select[name="day"] {
  margin-right: 20px;
}
input {
  width: 29.5vw;
  height: 45px;
  padding-left: 10px;
  font-size: 20px;
  color: black;
}
input::-webkit-input-placeholder {
  color: black;
}
button {
  background-color: #1abc9c;
  border: 1px solid black;
  color: white;
  height: 45px;
  border-radius: 20px;
  font-size: 20px;
  padding: 0 30px 0 30px;
  margin-bottom: 20px;
}
</style>
