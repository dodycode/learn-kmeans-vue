<template>
  <div class="table-mahasiswa">
    <table>
      <thead>
        <tr>
          <th>No.</th>
          <th>Tinggi Badan</th>
          <th>Berat Badan</th>
          <th>Lingkar Lengan Bawah</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(mahasiswa, index) in mahasiswaData" :key="index">
          <td>{{index + 1}}</td>
          <td>{{mahasiswa.tinggiBadan}}</td>
          <td>{{mahasiswa.beratBadan}}</td>
          <td>{{mahasiswa.lingkarLenganBawah}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ['mahasiswaData']
}
</script>

<style lang="scss" scoped>
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
</style>
