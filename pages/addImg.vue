<template>
  <form class="pt-4" action="add-img" method="POST" @submit.prevent="sendPhoto">
    <div class="form-group">
      <label for="exampleInputEmail1">Title</label>
      <input
        type="text"
        class="form-control"
        name="title"
        id="exampleInputEmail1"
        aria-describedby="emailHelp"
        placeholder="your title"
        v-model="title"
      />

      <label for="exampleInputEmail1 mt-4">Description</label>
      <input
        type="text"
        class="form-control"
        name="description"
        id="exampleInputEmail1"
        aria-describedby="emailHelp"
        placeholder="your description"
        v-model="description"
      />

      <input
        type="file"
        class="form-control-file mt-4"
        id="exampleFormControlFile1"
        @change="handelFileChange"
      />
    </div>

    <button type="submit" class="btn btn-primary mt-4 w-1">Submit</button>
  </form>

  <div class="wrapper mt-200">
    <div
      class="card"
      style="width: 18rem"
      v-for="card in cardData"
      :key="card.id"
    >
      <img
        class="card-img-top"
        :src="`http://localhost:4000/${card.src}`"
        :alt="card.title"
      />
      <div class="card-body mr-4">
        <h5 class="card-title">{{ card.title }}</h5>
        <p class="card-text">
          {{ card.description }}
        </p>
        <div class="button">
          <button class="btn btn-primary">Go somewhere</button>
          <button class="btn btn-danger" @click="removeCard(card.id)">
            remove
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onBeforeMount } from "vue";
import axios from "axios";

const file = ref("");
const title = ref("");
const description = ref("");
const cardData = ref(null);

function handelFileChange(event) {
  return (file.value = event.target.files[0]);
}

async function sendPhoto(event) {
  const formData = new FormData();
  formData.append("file", file.value);
  formData.append("title", title.value);
  formData.append("description", description.value);

  try {
    const response = await axios.post(
      "http://localhost:4000/add-img",
      formData,
      {
        headers: {
          "Content-Type": "multipart/form-data",
        },
      }
    );

    getImg();
    event.target.reset();
    file.value = "";
    title.value = "";
    description.value = "";
  } catch (error) {
    console.error("Ошибка при отправке файла", error);
  }
}

onBeforeMount(() => {
  getImg();
});

function getImg() {
  axios
    .get("http://localhost:4000/get-img")
    .then((response) => {
      cardData.value = response.data;
      console.log(cardData.value);
    })
    .catch((error) => {
      console.error("Ошибка при отправке запроса", error);
    });
}

function removeCard(id) {
  axios
    .delete(`http://localhost:4000/delet-img/${id}`)
    .then((response) => console.log(response))
    .catch((err) => console.log(err, "error"));

  const idx = cardData.value.findIndex((el) => el.id == id);
  cardData.value.splice(idx, 1);
}
</script>

<style lang="scss" scoped>
.button {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.wrapper {
  display: flex;
  align-items: center;
  justify-content: first baseline;
  flex-wrap: wrap;
}
.w-1 {
  width: 100%;
}
.mt-200 {
  margin-top: 200px;
}
</style>
