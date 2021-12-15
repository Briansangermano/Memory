<template>
  <div id="app">
    <div class="TimesContainer">
      <section>
        <input type="radio" v-model="timeIndex" :value="0" class="form-check-input">14Hrs
        <input type="radio" v-model="timeIndex" :value="1" class="form-check-input">16Hrs
        <input type="radio" v-model="timeIndex" :value="2" class="form-check-input">20Hrs
        <input type="radio" v-model="timeIndex" :value="3" class="form-check-input">23Hrs
      </section>
      <button @click="reset" class="btn btn-primary ResetButton">Reset</button>
    </div>
    <div class="Container">
      <div class="SalasContainer" v-for="(sala, indexSala) in data[0][1]" :key="indexSala">
        <span class="badge bg-secondary">Sala {{indexSala}}</span>
        <div class="ColumsContainer" v-for="(row, indexRow) in data" :key="indexRow">
          <div class="RowsContainer" v-for="(colums, indexColums) in data[indexRow]" :key="indexColums">
            <button :class="data[indexColums][indexRow][indexSala][timeIndex] ? 'btn btn-danger' : 'btn btn-success'" @click="savePlace({timeIndex, indexSala, indexRow, indexColums})">
              {{"C" + indexColums + "-" + "F" + indexRow}}
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import jsonData from "./json/data.json"

export default {
  name: 'App',
  data: () => {
    return {
      data: jsonData,
      timeIndex: 0,
    };
  },

  methods: {
    savePlace(value) {
      const place = this.data[value.indexColums][value.indexRow][value.indexSala];
      this.$set(place, value.timeIndex, !place[value.timeIndex]);
    },
    reset() {
      for (let i = 0; i < 10; i++) {
        for (let j = 0; j < 10; j++) {
          for (let f = 0; f < 5; f++) {
            for (let g = 0; g < 4; g++) {
              this.$set(this.data[i][j][f], g, false);
            }
          }
        }
      }
    },
  },
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .ColumsContainer {
    display: flex;
    margin: 2px;
  }

  .RowsContainer {
     margin: 2px;
  }

  .SalasContainer {
    padding: 20px;
  }

  .Container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  .TimesContainer {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  section {
    display: flex;
    align-items: center;
  }

  .form-check-input {
    margin: 10px;
    padding: 5px;
  }

  .ResetButton {
    margin-left: 40px;
  }

  .badge {
    font-size: 1.25em;
    margin-bottom: 10px;
  }
</style>
