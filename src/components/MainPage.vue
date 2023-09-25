<template>
  <div>
    <h1 :style="{ color: 'red' }">List of isekai school</h1>
    <div>
      <div>banyak yg mati adalah: {{ sumMati() }}</div>
      <div>yg menikah adalah: {{ sumMenikah() }}</div>
    </div>
    <div :style="{ display: 'flex', gap: '10px' }">
      <div>
        <div>Kelas 1</div>
        <table>
          <tr>
            <th>Nama</th>
            <th>Nilai</th>
          </tr>
          <tr v-for="item in allClass" :key="item.id">
            <td v-if="item.kelas === 1">{{ item.listNama }}</td>
            <td v-if="item.kelas === 1">{{ item.listNilai }}</td>
          </tr>
        </table>
      </div>
      <div>
        <div>Kelas 2</div>
        <table>
          <tr>
            <th>Nama</th>
            <th>Nilai</th>
          </tr>
          <tr v-for="item in allClass" :key="item.id">
            <td v-if="item.kelas === 2">{{ item.listNama }}</td>
            <td v-if="item.kelas === 2">{{ item.listNilai }}</td>
          </tr>
        </table>
      </div>
      <div>
        <div>Kelas 3</div>
        <table>
          <tr>
            <th>Nama</th>
            <th>Nilai</th>
          </tr>
          <tr v-for="item in allClass" :key="item.id">
            <td v-if="item.kelas === 3">{{ item.listNama }}</td>
            <td v-if="item.kelas === 3">{{ item.listNilai }}</td>
          </tr>
        </table>
      </div>
      <div>
        <div>Kelas 4</div>
        <table>
          <tr>
            <th>Nama</th>
            <th>Nilai</th>
          </tr>
          <tr v-for="item in allClass" :key="item.id">
            <td v-if="item.kelas === 4">{{ item.listNama }}</td>
            <td v-if="item.kelas === 4">{{ item.listNilai }}</td>
          </tr>
        </table>
      </div>
      <div>
        <div>Kelas 5</div>
        <table>
          <tr>
            <th>Nama</th>
            <th>Nilai</th>
          </tr>
          <tr v-for="item in allClass" :key="item.id">
            <td v-if="item.kelas === 5">{{ item.listNama }}</td>
            <td v-if="item.kelas === 5">{{ item.listNilai }}</td>
          </tr>
        </table>
      </div>
      <div>
        <div>Kelas 6</div>
        <table>
          <tr>
            <th>Nama</th>
            <th>Nilai</th>
          </tr>
          <tr v-for="item in allClass" :key="item.id">
            <td v-if="item.kelas === 6">{{ item.listNama }}</td>
            <td v-if="item.kelas === 6">{{ item.listNilai }}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      data: {},
      allClass: []
    }
  },
  async mounted() {
    await this.getApi()
  },
  methods: {
    sumMati() {
      let count = 0
      this.allClass.map((data) => {
        if (data.mati) return count++
      })
      return count
    },
    sumMenikah() {
      let count = 0
      this.allClass.map((data) => {
        if (data.kelas === 6 && data.listNilai % 7 === 0) return count++
      })
      return count
    },
    addClass(value, name) {
      if (name.includes('C') && name.includes('O')) return 6
      if (value >= 50 && value < 60) return 1
      else if (value >= 60 && value < 70) return 2
      else if (value >= 70 && value < 80) return 3
      else if (value >= 80 && value < 90) return 4
      else return 5
    },
    addMati(value) {
      // check bilangan prima
      for (let i = 2; i <= Math.sqrt(value); i++) {
        if (value % i === 0) return false
      }
      // check bulan ini (september)
      if (value % 10 !== 9) return false
      return true
    },
    changeData(data) {
      this.allClass = data.listNama.map((name, index) => ({
        listNama: data.listNama[index],
        listNilai: data.listNilai[index],
        kelas: this.addClass(data.listNilai[index], data.listNama[index]),
        mati: this.addMati(data.listNilai[index])
      }))
      // this.changeClass(this.allClass)
      // console.log(this.allClass)
    },
    getApi() {
      axios
        .get('http://ecocim-backend-theone.beit.co.id/api/ManualConfig/TestBEIT')
        .then((response) => {
          this.data = response.data
          this.changeData(response.data)
        })
        .catch((e) => console.log(e))
    }
  }
}
</script>

<style></style>
