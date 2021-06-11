<template>
    <div class="grid">
        <div class="row" v-for="(row, rowKey) in grid" :key="rowKey">
            <div class="cell" v-for="(col, colKey) in row" :key="colKey" @click="selectCell(rowKey, colKey)"  >
                {{ col }}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        moduloArr: Array
    },
    data() {
        return {
            grid: []
        };
    },
    watch: {
        moduloArr: function() {
            this.grid = Array(4).fill('?').map(() => Array(4).fill('?'))
        }
    },
    methods: {
        selectCell(row, col) {
            let moduloArr = this.moduloArr
            let newRow = this.grid[row].slice(0)
            if(newRow[col] == '?') {
                let randNr = moduloArr[Math.floor(Math.random() * moduloArr.length)]
                newRow[col] = (randNr == '?') ? "" : randNr
                this.$set(this.grid, row, newRow)
            }
        }
    }
};
</script>

<style>
.grid {
    margin-top: 20px;
}
.row {
    display: flex;
}
.row .cell {
    padding: 10px;
    -webkit-box-flex: 1;
    flex: 1;
    cursor: pointer;
    padding: 40px;
    text-align: center;
    border: 2px solid #ddd;
}
@media screen and (max-width: 480px) {
    .row .cell {
        padding: 20px;
    }
}
</style>
