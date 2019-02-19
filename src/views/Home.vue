<template>
  <div class="home">
    <TableMahasiswa :mahasiswa-data="mahasiswaData" />
    <TableBmiKerangka :bmi-kerangka-data="bmiKerangkaData" />
    <div class="table-cluster-container">
      <TableCluster
        v-for="(cluster, index) in clusterData"
        :key="index"
        :cluster="cluster"
        :index="index"
        :pusat-cluster="pusatClusterData[index]" />
    </div>
  </div>
</template>

<script>
import isEqual from 'lodash/isEqual'

// @ is an alias to /src
import TableMahasiswa from '@/components/TableMahasiswa.vue'
import TableBmiKerangka from '@/components/TableBmiKerangka.vue'
import TableCluster from '@/components/TableCluster.vue'

export default {
  name: 'home',
  components: {
    TableMahasiswa,
    TableBmiKerangka,
    TableCluster
  },
  data () {
    return {
      mahasiswaData: [
        { tinggiBadan: 163, beratBadan: 59, lingkarLenganBawah: 14 },
        { tinggiBadan: 170, beratBadan: 125, lingkarLenganBawah: 19 },
        { tinggiBadan: 164, beratBadan: 53, lingkarLenganBawah: 15 },
        { tinggiBadan: 166, beratBadan: 58, lingkarLenganBawah: 16 },
        { tinggiBadan: 167, beratBadan: 50, lingkarLenganBawah: 13 },
        { tinggiBadan: 168, beratBadan: 50, lingkarLenganBawah: 14 },
        { tinggiBadan: 173, beratBadan: 56, lingkarLenganBawah: 15 },
        { tinggiBadan: 168, beratBadan: 73, lingkarLenganBawah: 18 },
        { tinggiBadan: 177, beratBadan: 60, lingkarLenganBawah: 15 },
        { tinggiBadan: 168, beratBadan: 52, lingkarLenganBawah: 15 },
        { tinggiBadan: 159, beratBadan: 58, lingkarLenganBawah: 15 },
        { tinggiBadan: 167, beratBadan: 75, lingkarLenganBawah: 16 },
        { tinggiBadan: 170, beratBadan: 72, lingkarLenganBawah: 16 },
        { tinggiBadan: 172, beratBadan: 68, lingkarLenganBawah: 15 },
        { tinggiBadan: 165, beratBadan: 73, lingkarLenganBawah: 18 },
        { tinggiBadan: 169.5, beratBadan: 55, lingkarLenganBawah: 14 },
        { tinggiBadan: 160, beratBadan: 54, lingkarLenganBawah: 15 },
        { tinggiBadan: 173, beratBadan: 56, lingkarLenganBawah: 14 },
        { tinggiBadan: 162, beratBadan: 54, lingkarLenganBawah: 15 },
        { tinggiBadan: 169, beratBadan: 79, lingkarLenganBawah: 17 }
      ],
      pusatClusterData: [
        [ // First random data
          { bmi: 20, ukuranKerangka: 9 },
          { bmi: 23, ukuranKerangka: 10 },
          { bmi: 27, ukuranKerangka: 11 }
        ]
      ],
      clusterData: []
    }
  },
  computed: {
    bmiKerangkaData () {
      return this.mahasiswaData.map(mahasiswa => {
        const heightInMeter = mahasiswa.tinggiBadan / 100
        const bmi = parseFloat((mahasiswa.beratBadan / Math.pow(heightInMeter, 2)).toFixed(2))
        const ukuranKerangka = parseFloat((mahasiswa.tinggiBadan / mahasiswa.lingkarLenganBawah).toFixed(2))
        return { bmi, ukuranKerangka }
      })
    }
  },

  methods: {
    doCluster (pusatCluster) {
      const cluster = this.bmiKerangkaData.map(item => {
        const bmiKerangka = { ...item } // Assign new object so it will not reference

        bmiKerangka.cluster = []

        let selectedCluster = {}
        pusatCluster.forEach((data, index) => {
          const count = Math.pow(bmiKerangka.bmi - data.bmi, 2) + Math.pow(bmiKerangka.ukuranKerangka - data.ukuranKerangka, 2)
          const square = Math.sqrt(count)
          const value = parseFloat(square.toFixed(2))
          bmiKerangka.cluster.push({ value })

          if (selectedCluster.value == null || value < selectedCluster.value) {
            selectedCluster.value = value // For comparing value
            selectedCluster.index = index // For setup the position of selected cluster
          }
        })
        bmiKerangka.cluster[selectedCluster.index].selected = true

        return bmiKerangka
      })
      this.clusterData.push(cluster)
    },

    getNextPusatCluster (cluster) {
      const newPusatCluster = []
      for (let i = 0; i < this.pusatClusterData[0].length; i++) {
        let totalBmi = { value: 0, length: 0 }
        let totalUkuranKerangka = { value: 0, length: 0 }
        cluster.forEach(item => {
          if (item.cluster[i].selected) {
            totalBmi.value += item.bmi
            totalBmi.length++
            totalUkuranKerangka.value += item.ukuranKerangka
            totalUkuranKerangka.length++
          }
        })

        const averageBmi = parseFloat((totalBmi.value / totalBmi.length).toFixed(2))
        const averageUkuranKerangka = parseFloat((totalUkuranKerangka.value / totalUkuranKerangka.length).toFixed(2))
        newPusatCluster.push({ bmi: averageBmi, ukuranKerangka: averageUkuranKerangka })
      }

      this.pusatClusterData.push(newPusatCluster)
    },

    checkEqualsClusterData (cluster1, cluster2) {
      const cluster1Selected = []
      const cluster2Selected = []

      cluster1.forEach(item => {
        item.cluster.forEach((clusterItem, index) => {
          if (clusterItem.hasOwnProperty('selected')) {
            cluster1Selected.push(index)
          }
        })
      })

      cluster2.forEach(item => {
        item.cluster.forEach((clusterItem, index) => {
          if (clusterItem.hasOwnProperty('selected')) {
            cluster2Selected.push(index)
          }
        })
      })

      return isEqual(cluster1Selected, cluster2Selected)
    }
  },

  mounted () {
    this.doCluster(this.pusatClusterData[0])
    this.getNextPusatCluster(this.clusterData[0])
    this.doCluster(this.pusatClusterData[1])

    if (this.checkEqualsClusterData(this.clusterData[0], this.clusterData[1])) {

    }
  }
}
</script>

<style lang="scss">
.home {
  padding: 32px;
}

.table-design {
  display: inline-block;

  table {
    width: auto;
  }

  table tr th {
    text-align: center;
  }

  table tr td {
    text-align: center;

    &.selected {
      background: #42b983;
      color: #FFFFFF;
    }
  }
}

.table-cluster-container {
  margin-top: 64px;
}
</style>
