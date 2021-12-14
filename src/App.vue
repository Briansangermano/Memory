<template>
  <div id="app">
    <div class="TimesContainer">
      <section>
        <input type="radio" v-model="timeIndex" :value="0" class="ButtonTime">14Hrs
        <input type="radio" v-model="timeIndex" :value="1" class="ButtonTime">16Hrs
        <input type="radio" v-model="timeIndex" :value="2" class="ButtonTime">20Hrs
        <input type="radio" v-model="timeIndex" :value="3" class="ButtonTime">23Hrs
      </section>
    </div>
    <div class="Container">
      <div class="SalasContainer" v-for="(sala, indexSala) in data[0][1]" :key="indexSala">
        <p>Sala {{indexSala}}</p>
        <div class="ColumsContainer" v-for="(row, indexRow) in data" :key="indexRow">
          <div class="RowsContainer" v-for="(colums, indexColums) in data[indexRow]" :key="indexColums">
            <button :disabled="data[indexColums][indexRow][indexSala][timeIndex]" @click="savePlace({timeIndex, indexSala, indexRow, indexColums})">
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
      this.data[value.indexColums][value.indexRow][value.indexSala][value.timeIndex] = true;
    }
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
  }

  .ButtonTime {
    margin: 10px;
    padding: 5px;
  }
</style>
