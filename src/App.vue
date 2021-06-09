<template>
  <div id="app">
    <Form />
  </div>
</template>

<script>
import Form from "./components/Form";

export default {
  name: "App",
  components: {
    Form
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #e2e2e2;
}
</style>
