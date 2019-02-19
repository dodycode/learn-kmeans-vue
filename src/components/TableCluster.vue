<template>
  <div class="table-cluster table-design">
    <h4>Iterasi {{index + 1}}</h4>
    <table>
      <thead>
        <tr>
          <th>No.</th>
          <th>BMI</th>
          <th>Ukuran Kerangka</th>
          <th v-for="(data, index) in cluster[0].cluster" :key="index">
            C{{index + 1}}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(data, index) in cluster" :key="index">
          <td>{{index + 1}}</td>
          <td>{{data.bmi}}</td>
          <td>{{data.ukuranKerangka}}</td>
          <td v-for="(item, index) in data.cluster" :key="index" :class="{ selected: item.selected }">
            {{ item.value }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ['cluster', 'index']
}
</script>

<style lang="scss" scoped>

</style>
