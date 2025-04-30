<template>
  <div id="app">
    <h1>Kegiatan Ku</h1>

    <!-- Form untuk menambah kegiatan -->
    <input v-model="newActivity" type="text" placeholder="Masukkan kegiatan baru" />
    <button @click="addActivity">Tambah Kegiatan</button>

    <!-- Filter: tampilkan hanya kegiatan belum selesai -->
    <div style="margin-top: 20px;">
      <label>
        <input type="checkbox" v-model="showOnlyIncomplete" />
        Tampilkan hanya kegiatan yang belum selesai
      </label>
    </div>

    <!-- Daftar kegiatan -->
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index">
        <input type="checkbox" v-model="activity.completed" />
        <span :class="{ completed: activity.completed }">{{ activity.name }}</span>
        <button @click="removeActivity(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: [],
      showOnlyIncomplete: false
    };
  },
  computed: {
    filteredActivities() {
      return this.showOnlyIncomplete
        ? this.activities.filter(activity => !activity.completed)
        : this.activities;
    }
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ name: this.newActivity.trim(), completed: false });
        this.newActivity = '';
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}

input[type="text"] {
  padding: 8px;
  margin-right: 10px;
}

button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
  margin-left: 10px;
}

button:hover {
  background-color: #45a049;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 10px 0;
  font-size: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.completed {
  text-decoration: line-through;
  color: #888;
}

button:nth-child(3) {
  background-color: #f44336;
}

button:nth-child(3):hover {
  background-color: #e53935;
}
</style>
