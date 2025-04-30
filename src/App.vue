<template>
  <div id="app">
    <div class="card">
      <h1 class="title">📋 Daftar Kegiatan</h1>

      <!-- Form tambah kegiatan -->
      <div class="input-group">
        <input
          v-model="newActivity"
          type="text"
          placeholder="Tambahkan kegiatan baru..."
          @keyup.enter="addActivity"
        />
        <button @click="addActivity">+</button>
      </div>

      <!-- Filter checkbox -->
      <div class="filter">
        <label>
          <input type="checkbox" v-model="showOnlyIncomplete" />
          Hanya tampilkan kegiatan yang belum selesai
        </label>
      </div>

      <!-- Daftar kegiatan -->
      <transition-group name="fade" tag="ul" class="list">
        <li
          v-for="(activity, index) in filteredActivities"
          :key="activity.name + index"
          class="list-item"
        >
          <label class="checkbox-label">
            <input type="checkbox" v-model="activity.completed" />
            <span :class="{ completed: activity.completed }">{{ activity.name }}</span>
          </label>
          <button class="delete-btn" @click="removeActivity(index)">🗑</button>
        </li>
      </transition-group>
    </div>
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
      const name = this.newActivity.trim();
      if (name) {
        this.activities.push({ name, completed: false });
        this.newActivity = '';
      }
    },
    removeActivity(index) {
      this.activities.splice(index, 1);
    }
  }
};
</script>

<style scoped>
body {
  margin: 0;
  background: #f5f7fa;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

#app {
  display: flex;
  justify-content: center;
  align-items: start;
  padding: 40px 20px;
  min-height: 100vh;
}

.card {
  background: white;
  padding: 30px 40px;
  border-radius: 16px;
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  width: 100%;
}

.title {
  margin: 0 0 20px;
  color: #333;
  font-size: 28px;
  font-weight: bold;
  text-align: center;
}

.input-group {
  display: flex;
  gap: 12px;
  margin-bottom: 20px;
}

input[type="text"] {
  flex: 1;
  padding: 12px 16px;
  border-radius: 10px;
  border: 1px solid #ccc;
  font-size: 16px;
}

button {
  padding: 0 18px;
  background: #4caf50;
  color: white;
  font-size: 22px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: background 0.2s;
}

button:hover {
  background: #43a047;
}

.filter {
  text-align: left;
  margin-bottom: 15px;
  font-size: 14px;
  color: #555;
}

.list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #f9fbfd;
  padding: 12px 16px;
  border-radius: 10px;
  margin-bottom: 10px;
  transition: all 0.3s ease;
  border: 1px solid #e0e0e0;
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 10px;
  flex: 1;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

.delete-btn {
  background: none;
  color: #e53935;
  font-size: 18px;
  border: none;
  cursor: pointer;
  transition: transform 0.2s;
}

.delete-btn:hover {
  transform: scale(1.2);
}

/* Animasi */
.fade-enter-active,
.fade-leave-active {
  transition: all 0.4s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
</style>
