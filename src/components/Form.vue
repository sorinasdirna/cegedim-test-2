<template>
    <div>
        <form @submit.prevent="handleSubmit">
            <label>Introduceti un sir de numere cuprinse intre 100 si 999 separate prin
                virgula:</label>
            <input type="text" v-model="inputArr" placeholder="Ex: 110, 120, 130, 280, 780, 510, 505, 605, 720, 230, 210, 275" />
            <button>Calculate</button>
            <div class="output" v-show="showOutput">
                <div class="maxim">Maximele din clase: {{ outputArr }}</div>
                <div class="modulo">Modulo: {{ moduloArr }}</div>
                <div class="grid">
                    <div class="row" v-for="(row, rowKey) in grid" :key="rowKey">
                        <div class="cell" v-for="(col, colKey) in row" :key="colKey" @click="checkGridCell(rowKey, colKey)"  >
                            {{ col }}
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>
<script>
export default {
    data() {
        return {
            inputArr: "110, 120, 130, 280, 780, 510, 505, 605, 720, 230, 210, 275", // 110, 120, 130, 280, 780, 510, 505, 605, 720, 230, 210, 275
            outputArr: [], // 130, 280, 510, 605, 780
            moduloArr: [], // A, U, Q, H, A
            showOutput: false,
            gridPositionsRand: [],
            grid: []
        };
    },
    methods: {
        handleSubmit() {
            // maxim
            this.outputArr = this.getMaxim(this.inputArr)

            // modulo
            this.moduloArr = this.getModulo(this.outputArr)

            // matrice
            this.grid = this.fillGridCells()

            // to display on click
            this.gridPositionsRand = this.fillGridPositionsRand(this.moduloArr)

            // afisare
            this.showOutput = true
        },
        getMaxim(inputArr) {
            inputArr = inputArr.split(",").map(Number);
            let outputArr = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0];
            for (let i = 0; i < inputArr.length; i++) {
                let element = inputArr[i];
                let position = Math.floor(element / 100);
                if (outputArr[position] < element) {
                    outputArr[position] = element;
                }
            }
            return outputArr.filter(item => item !== 0)
        },
        getModulo(outputArr) {
            return outputArr.map(nr => String.fromCharCode((nr % 26) + 65))
        },
        fillGridCells() {
            return Array(4).fill('?').map(() => Array(4).fill('?'))
        },
        fillGridPositionsRand(moduloArr) {
            let gridPositionsRand = new Array(16-moduloArr.length).fill("?")
            return [...moduloArr, ...gridPositionsRand]
        },
        checkGridCell(row, col) {
            let newRow = this.grid[row].slice(0)
            if(newRow[col] == '?' && this.gridPositionsRand.length > 0) {
                let randNr = this.gridPositionsRand.splice(Math.floor(Math.random()*this.gridPositionsRand.length), 1).toString()
                newRow[col] = (randNr == '?') ? "" : randNr
                this.$set(this.grid, row, newRow)
            }
        }
    }
};
</script>

<style>
form {
    max-width: 600px;
    margin: 40px auto;
    background: #fff;
    padding: 20px;
}
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
.output {
    border: 3px solid #bbb;
    padding: 15px;
    margin-top: 15px;
    background: #f2f2f2;
}
.maxim {
    margin-bottom: 10px;
}
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
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid #ddd;
}
@media screen and (max-width: 480px) {
    .row .cell {
        height: 60px
    }
    input[type="text"] {
        width: 100%;
        margin-bottom: 10px;
    }
    button {
        width: 100%;
    }
}
</style>