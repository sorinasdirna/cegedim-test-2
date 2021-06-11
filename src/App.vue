<template>
  <div id="app" class="app">
    <Form v-on:formData="getFormData($event)" />
    <Output v-bind:inputArr="inputArr" v-show="showOutput" />
  </div>
</template>

<script>
import Form from "./components/Form"
import Output from "./components/Output"

export default {
    name: "App",
    data() {
        return {
            inputArr: [], 
            showOutput: false
        };
    },
    components: {
        Form,
        Output
    },
    methods: {
        getFormData(inputArr) {
            this.inputArr = inputArr
            this.showOutput = true
        },
       
    }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
    margin: 0;
}

.app {
    max-width: 600px;
    margin: 40px auto;
    background: #fff;
    padding: 20px;
    border: 1px solid #e2e2e2;
}

@media screen and (max-width: 768px) {
    .app {
        max-width: 100%;
        margin: 0;
    }
}
</style>
