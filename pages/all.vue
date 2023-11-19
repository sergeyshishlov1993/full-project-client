<template>
  <div>
    <ul class="list-group">
      <li class="list-group-item" v-for="user in userList" :key="user.id">
        {{ user.email }}
        <span>
          {{ user.password }}
        </span>
      </li>
    </ul>

    <button class="btn btn-primary mt-30" @click="getList">get list</button>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";
import axios from "axios";

const userList = ref([]);
function getList() {
  axios
    .get("http://localhost:4000/all")
    .then((response) => {
      userList.value = response.data;
      console.log(response);
    })
    .catch((error) => {
      console.error("Ошибка при отправке запроса", error);
    });
}
</script>

<style lang="scss" scoped>
ul {
  margin: 0 auto;
  margin-top: 200px;
  li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    span {
      display: block;
    }
  }
}

.mt-30 {
  margin-top: 30px;
  width: 100%;
}
</style>
