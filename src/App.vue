<template>
  <div class="container">
    <h1 class="title">TO-DO LIST KEGIATAN</h1>
    <form @submit.prevent="addTask" class="task-form">
      <input type="text" v-model="newTask" placeholder="Tambahkan Kegiatan Baru">
      <button>Tambahkan</button>
    </form>
    <ul class="task-list">
      <li v-for="(task, index) in tasksFiltered" :key="index" class="task-item">
        <button @click="completeTask(index)" :class="{ completedButton: task.completed }">
          <!-- Mengubah warna ceklis menjadi putih -->
          <span style="color: #fff;">✔️</span>
        </button>
        <span @click="completeTask(index)" :class="{ completed: task.completed }">{{ task.title }}</span>
        <button @click="deleteTask(index)">Hapus</button>
      </li>
    </ul>
    <div class="filter-container">
      <input type="checkbox" id="completedOnly" v-model="completedOnly">
      <label for="completedOnly">Tampilkan yang belum selesai saja</label>
    </div>
    <div class="ig-info">
      <span>@nrizh31</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { title: 'ngoding', completed: false },
        { title: 'healing sejenak after dipush tugas', completed: false },
      ],
      newTask: '',
      completedOnly: false
    }
  },
  computed: {
    tasksFiltered() {
      if (this.completedOnly) {
        return this.tasks.filter(task => !task.completed)
      } else {
        return this.tasks
      }
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ title: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    completeTask(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
}
</script>

<style>
.container {
  padding: 20px;
}

.title {
  color: #DCDCDC;
  font-weight: bold;
  margin-bottom: 20px;
  text-align: center;
}

.task-form {
  display: flex;
  margin-bottom: 20px;
}

input[type="text"] {
  padding: 5px;
  font-size: 16px;
  flex: 1;
  margin-right: 10px;
}

button {
  padding: 5px 10px;
  font-size: 16px;
  background-color: hsl(249, 85%, 64%);
  color: #fff;
  border: none;
  cursor: pointer;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  background-color: #000; /* Latar belakang hitam */
  color: #fff; /* Warna teks putih */
  border: 1px solid #fff; /* Border putih */
  padding: 10px; /* Padding untuk ruang di dalam border */
}

.task-item span {
  flex: 1;
  cursor: pointer;
}

span.completed {
  text-decoration: line-through;
}

button.completedButton {
  background-color: #4CAF50;
  color: #fff;
  margin-right: 10px;
}

button.completedButton.completed {
  background-color: #009688;
}

.filter-container {
  display: flex;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5); /* Latar belakang hitam dengan transparansi 50% */
  color: #fff; /* Warna teks putih */
  border: 1px solid #fff; /* Border putih */
  padding: 10px; /* Padding untuk ruang di dalam border */
  margin-top: 20px;
  border-radius: 15px; /* Sudut border melengkung */
}

.filter-container label {
  margin-left: 10px;
}

.ig-info {
  position: fixed;
  right: 20px;
  bottom: 20px;
  background-color: rgba(0, 0, 0, 0.5); /* Latar belakang hitam dengan transparansi 50% */
  color: #fff; /* Warna teks putih */
  border: 1px solid #fff; /* Border putih */
  padding: 10px; /* Padding untuk ruang di dalam border */
  border-radius: 15px; /* Sudut border melengkung */
}

@media (max-width: 600px) {
  .container {
    padding: 10px;
  }

  .title {
    font-size: 1.5em;
  }

  .task-form {
    flex-direction: column;
  }

  input[type="text"] {
    margin-right: 0;
    margin-bottom: 10px;
  }

  .task-item {
    flex-direction: column;
    align-items: flex-start;
  }

  .filter-container {
    flex-direction: column;
    align-items: flex-start;
  }

  .filter-container label {
    margin-left: 0;
    margin-top: 10px;
  }
}
</style>
