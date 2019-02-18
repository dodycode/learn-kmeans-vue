<template>
  <div class="home">
    <TableMahasiswa :mahasiswa-data="mahasiswaData" />
  </div>
</template>

<script>
// @ is an alias to /src
import TableMahasiswa from '@/components/TableMahasiswa.vue'

export default {
  name: 'home',
  components: {
    TableMahasiswa
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
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.home {
  padding: 32px;
}
</style>
