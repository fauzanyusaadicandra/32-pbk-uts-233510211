<template>
  <div id="app">
    <h1>Kegiatan Ku</h1>

    <!-- Form untuk menambah kegiatan -->
    <input v-model="newActivity" type="text" placeholder="Masukkan kegiatan baru" />
    <button @click="addActivity">Tambah Kegiatan</button>

    <!-- Menampilkan daftar kegiatan yang sudah ditambahkan -->
    <ul>
      <li v-for="(activity, index) in activities" :key="index">
        <input type="checkbox" v-model="activity.completed" /> <!-- Checkbox untuk menandai kegiatan selesai -->
        <span :class="{ completed: activity.completed }">{{ activity.name }}</span> <!-- Menandai dengan CSS jika selesai -->
        <button @click="removeActivity(index)">Hapus</button> <!-- Tombol hapus kegiatan -->
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
        this.activities.push({ name: this.newActivity.trim(), completed: false }); // Menambahkan kegiatan baru dengan status completed false
        this.newActivity = ''; // Reset input setelah ditambah
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1); // Menghapus kegiatan berdasarkan index
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

button:nth-child(2) {
  background-color: #f44336; /* Merah untuk tombol hapus */
}

button:nth-child(2):hover {
  background-color: #e53935; /* Warna merah lebih gelap saat hover */
}

/* Styling untuk kegiatan yang sudah selesai */
.completed {
  text-decoration: line-through; /* Garis tengah untuk menunjukkan kegiatan selesai */
  color: #888;
}
</style>
