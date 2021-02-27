<template>
  <div id="app">
    <h1 v-if="activeTask === 1">Осталось совсем немного!</h1>
    <h1 v-else-if="activeTask === 0">Вы превосходны!</h1>
    <h1 v-else>Всего задач: {{ activeTask }}</h1>
    <form action="#">
      <fieldset>
        <legend>Задачи</legend>
        <div class="task" v-for="(task, index) in tasks" :key="index">
          <label :class="{'task-done': task.done}">
            <input type="checkbox" :checked="task.done" @click="setDone(index)">
            {{ task.title }}
          </label>
        </div>
      </fieldset>
    </form>

    <form action="#" @submit.stop="addTask">
    <label>
    <input type="text" v-model="message">
    </label>
    <button>Add</button>
    </form>
    <transition name="done-picture">
    <img v-show="activeTask ===0" src="https://cdn.rtl.hu/44/31/mit-nezunk-ma-vasarnap-2020-02-16_image_041e392f6447d380b2699aa20398_16-9?size=2" alt="13">
    </transition>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {},
  data() {
    return {
      message: '',
      tasks: [
        { title: 'create Vue app', done: true },
        { title: 'create React app', done: true },
        { title: 'create Angular app', done: false },
      ],
    };
  },

  methods: {
    addTask() {
      if (this.message) {
        this.tasks.push({ title: this.message, done: false });
      }
      this.message = '';
    },
    setDone(index) {
      this.tasks[index].done = !this.tasks[index].done;
    },
  },

  computed: {
    activeTask() {
      return this.tasks.filter((task) => !task.done).length;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul,ol {
  padding: 0;
  list-style: none;
}
.task-done {
  text-decoration: line-through;
}

.done-picture-enter-active,.done-picture-leave-active {
  transition-timing-function: ease-in-out;
  transition-duration: .5s;
  transition-property: opacity, transform;
}

.done-picture-enter, .done-picture-leave-to {
  opacity: 0;
  transform: translateY(200px);
}
</style>
