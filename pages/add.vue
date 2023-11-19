<template>
  <form action="/add" method="POST" @submit.prevent="sendForm">
    <h2>Form Control</h2>
    <div class="form-group">
      <label for="exampleInputEmail1">Email address</label>
      <input
        type="email"
        class="form-control"
        name="email"
        id="exampleInputEmail1"
        aria-describedby="emailHelp"
        placeholder="Enter email"
        @input="(event) => getInputValue(event, 'email')"
      />
      <small id="emailHelp" class="form-text text-muted"
        >We'll never share your email with anyone else.</small
      >
    </div>
    <div class="form-group">
      <label for="exampleInputPassword1">Password</label>
      <input
        type="password"
        class="form-control"
        name="password"
        id="exampleInputPassword1"
        placeholder="Password"
        @input="(event) => getInputValue(event, 'password')"
      />
    </div>
    <div class="form-check">
      <input type="checkbox" class="form-check-input" id="exampleCheck1" />
      <label class="form-check-label" for="exampleCheck1">Check me out</label>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
  </form>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";
const email = ref("");
const password = ref("");

function getInputValue(event, name) {
  switch (name) {
    case "email":
      email.value = event.target.value;
      break;

    case "password":
      password.value = event.target.value;
      break;
  }
}

async function sendForm(event) {
  const test = {
    email: email.value,
    password: password.value,
  };

  await axios
    .post("http://localhost:4000/add", JSON.stringify(test), {
      headers: {
        "Content-Type": "application/json",
      },
    })
    .then((response) => {
      console.log(response.data);
    })
    .catch((error) => {
      console.error("Ошибка при отправке запроса", error);
    });

  email.value = "";
  password.value = "";
  event.target.reset();
}
</script>

<style lang="scss" scoped>
form {
  padding: 30px;
  margin: 0 auto;
  margin-top: 200px;
  width: 700px;
  border: 1px solid black;
  h2 {
    text-align: center;
    margin-bottom: 50px;
  }
}
</style>
