<template>
  <div class="table-bmi-kerangka table-design">
    <h4>Hasil perhitungan nilai BMI dan ukuran kerangka setiap data</h4>
    <table>
      <thead>
        <tr>
          <th>No.</th>
          <th>BMI</th>
          <th>Ukuran Kerangka</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(bmiKerangka, index) in bmiKerangkaData" :key="index">
          <td>{{index + 1}}</td>
          <td>{{bmiKerangka.bmi}}</td>
          <td>{{bmiKerangka.ukuranKerangka}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ['bmiKerangkaData']
}
</script>

<style lang="scss" scoped>
.table-bmi-kerangka {
  margin-left: 120px;
}
</style>
