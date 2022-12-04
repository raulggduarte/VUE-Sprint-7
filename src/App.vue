<template>
  <router-view/>
</template>

<script>
  export default {
    name: "App",
  }
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.routerBtn {
  padding: 10px 20px;
  background-color: rgb(217, 154, 36);
  border: none;
  border-radius: 10px;
  text-decoration: none;
  color: black;
  font-size: large;
  text-align: center;
}
.routerBtn:hover {
  color: black;
  background-color: white;
  box-shadow:inset 0px 0px 0px 2px rgb(217, 154, 36);
}
</style>
