<template>

  <h2>Lista / Tarefas</h2>
  
  <br/>

  <button @click="handleShowHideList">CLICK</button>

  <hr/>

  <input 
    type="text" 
    @keyup.enter="addTask"
    v-focus 
    v-model="currentTask" 
  />

  <ul v-if="showList">
    <li
      v-for="(task, index) in tasks"
      @dbclick="complete(task)"
      class="task-inter"
      :class="{
        'line-through': task.isDone,
      }"
      :key=" `${task} -> ${index}` "
    >
      {{ task.name }}
      <button 
        @click=" remove(task) "
      >&times;</button>
    </li>
  </ul>

  <p v-else>Lista oculta!</p>

  <hr/>

  

</template>


<script scoped>

  const focus = {
    inserted: (el) => {
      el.focus()
    }
  }

  export default {

    directives: {
      focus
    },
    data: () => ({
      currentTask: '',
      showList: false,
      tasks: [
        { name: 'Estudar JS', isDone: false }
      ]
    }),
    methods: {
      handleShowHideList () {
        this.showList = !this.showList
      },
      addTask () {
        this.tasks.push({
          name: this.currentTask,
          isDone: false
        })
        this.currentTask = ''
      },
      complete (task) {
        this.tasks = this.tasks.map(e => {
          if (e.name === task.name) {
            return { ...e, isDone: !e.isDone }
          }
          return { ...e }
        })
      },
      remove (task) {
        this.tasks = this.tasks.filter(e => e.name !== task.name)
        console.log('taks', task)
      }
    }
  }

</script>


<style scoped>
.line-through {
  text-decoration: line-through;
}
.task-inter {
  cursor: pointer;
}
</style>