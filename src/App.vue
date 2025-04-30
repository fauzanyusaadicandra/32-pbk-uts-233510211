<template>
  <div id="app">
    <h1>Kegiatan Ku</h1>

    <!-- Form untuk menambah kegiatan -->
    <input v-model="newActivity" type="text" placeholder="Masukkan kegiatan baru" />
    <button @click="addActivity">Tambah Kegiatan</button> <!-- Menambahkan tombol untuk menambah kegiatan -->

    <!-- Menampilkan daftar kegiatan yang sudah ditambahkan -->
    <ul>
      <li v-for="(activity, index) in activities" :key="index">
        {{ activity }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '', // Untuk menampung input kegiatan baru
      activities: []    // Array untuk menyimpan daftar kegiatan
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push(this.newActivity.trim()); // Menambahkan kegiatan ke array
        this.newActivity = ''; // Reset input setelah ditambah
      }
    }
  }
};
</script>

<style>
/* Styling dasar */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}

input {
  padding: 8px;
  margin-right: 10px;
}

button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 5px 0;
  font-size: 18px;
}
</style>
