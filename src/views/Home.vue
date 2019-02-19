<template>
  <div class="home">
    <TableMahasiswa :mahasiswa-data="mahasiswaData" />
    <TableBmiKerangka :bmi-kerangka-data="bmiKerangkaData" />
    <TableCluster v-for="(cluster, index) in clusterData" :key="index" :cluster="cluster" />
  </div>
</template>

<script>
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
        [
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
        const bmi = (mahasiswa.beratBadan / Math.pow(heightInMeter, 2)).toFixed(2)
        const ukuranKerangka = (mahasiswa.tinggiBadan / mahasiswa.lingkarLenganBawah).toFixed(2)
        return { bmi, ukuranKerangka }
      })
    }
  },

  methods: {
    doCluster (pusatCluster) {
      const cluster = this.bmiKerangkaData.map(bmiKerangka => {
        bmiKerangka.cluster = []
        pusatCluster.forEach(data => {
          const count = Math.pow(bmiKerangka.bmi - data.bmi, 2) + Math.pow(bmiKerangka.ukuranKerangka - data.ukuranKerangka, 2)
          const square = Math.sqrt(count)
          bmiKerangka.cluster.push(square.toFixed(2))
        })

        return bmiKerangka
      })
      this.clusterData.push(cluster)
    }
  },

  mounted () {
    this.pusatClusterData.forEach(pusatCluster => {
      this.doCluster(pusatCluster)
    })
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
    text-align: right;

    &:first-child {
      text-align: center;
    }
  }
}
</style>
