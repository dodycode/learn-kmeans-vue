<template>
  <div class="conclusion">
    <h2>Kesimpulan</h2>
    <ul>
      <li v-for="(item, index) in pusatCluster" :key="index">
        Pusat Cluster {{index + 1}}:
        <ul>
          <li>BMI: {{item.bmi}}</li>
          <li>Ukuran Kerangka: {{item.ukuranKerangka}}</li>
        </ul>
        <p>Kelompok mahasiswa dengan <b>BMI {{bmi(item.bmi)}}</b> dan <b>kerangka {{ukuranKerangka(item.ukuranKerangka)}}</b></p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['pusatCluster'],

  computed: {
    bmi () {
      return number => {
        let desc
        if (number < 18.5) desc = 'kurang'
        else if (number >= 18.5 && number <= 22.9) desc = 'normal'
        else if (number >= 23 && number <= 24.9) desc = 'obesitas ringan'
        else if (number >= 25 && number <= 29.9) desc = 'obesitas sedang'
        else desc = 'obesitas berat'

        return desc
      }
    },

    ukuranKerangka () {
      return number => {
        let desc
        if (number < 9.6) desc = 'kecil'
        else if (number >= 9.6 && number <= 10.4) desc = 'sedang'
        else desc = 'besar'

        return desc
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.conclusion {
  margin-top: 64px;
}
</style>
