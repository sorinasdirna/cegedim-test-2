<template>
    <div class="output">
        <div class="output_maxim">Maximele din clase: <strong>{{ maximArr }}</strong></div>
        <div class="output_modulo">Modulo: <strong>{{ moduloArr }}</strong></div>
        <div class="output_grid">
            <Grid v-bind:moduloArr="moduloArr" />
        </div>
    </div>

  </div>
</template>

<script>
import Grid from "./Grid"

export default {
    props: {
        inputArr: Array,
    },
    data() {
        return {
            maximArr: [], // 130, 280, 510, 605, 780
            moduloArr: [], // A, U, Q, H, A
            grid: []
        };
    },
    components: {
        Grid
    },
    watch: {
        inputArr: function() {
            this.maximArr = this.getMaxim(this.inputArr)
            this.moduloArr = this.getModulo(this.maximArr)
        }
    },
    methods: {
        getMaxim(inputArr) {
            let maximArr = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0];
            for (let i = 0; i < inputArr.length; i++) {
                let element = inputArr[i];
                let position = Math.floor(element / 100);
                if (maximArr[position] < element) {
                    maximArr[position] = element;
                }
            }
            return maximArr.filter(item => item !== 0)
        },
        getModulo(maximArr) {
            return maximArr.map(nr => String.fromCharCode((nr % 26) + 65))
        }
    }
};
</script>

<style>
.output {
    border: 3px solid #bbb;
    padding: 15px;
    margin-top: 15px;
    background: #f2f2f2;
}
.output_maxim {
    margin-bottom: 10px;
}
@media screen and (max-width: 480px) {
    .output >div >strong {
        display: block;
        margin: 5px 0;
    }
}
</style>
