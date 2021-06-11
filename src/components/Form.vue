<template>
    <form>
        <label>Introduceti un sir de numere cuprinse intre 100 si 999 separate prin
            virgula:</label>
        <input type="text" v-model="inputArr" placeholder="Ex: 110, 120, 130, 280, 780, 510, 505, 605, 720, 230, 210, 275" />
        <button  @click.prevent="handleForm">Calculate</button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            inputArr: "110, 120, 130, 280, 780, 510, 505, 605, 720, 230, 210, 275"
        }     
    },
    methods: {
       handleForm() {
           let inputArr = this.inputArr.split(",").map(Number);
           this.$emit('formData', inputArr)
       }
    }
};
</script>

<style>
label {
    display: block;
    margin-bottom: 5px;
}
input[type="text"] {
    border: 2px solid #e2e2e2;
    width: calc(100% - 100px);
    padding: 10px 15px;
    display: inline-block;
}
button {
    padding: 10px;
    width: 90px;
    display: inline-block;
    cursor: pointer;
}
@media screen and (max-width: 768px) {
    input[type="text"] {
        width: 100%;
        margin-bottom: 10px;
    }
    button {
        width: 100%;
    }
}
</style>