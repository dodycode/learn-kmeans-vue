<template>
  <div class="table-mahasiswa table-design">
    <h4>Contoh Data Mahasiswa (Asumsi Data Putra)</h4>
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

</style>
