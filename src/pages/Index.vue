<template>
  <q-page padding class="flex">
    <div class="row">
    <h3 class="col-12">Tasks</h3>
    <div class="col-12 row">
      <q-select v-model="usuarioSelecionado" :options="users" option-value="id" option-label="name" label="Usuários" @input="listTasks" />
    </div>
    <q-list class="col-12 row" bordered separator>
      <q-item
        class="col-12"
        clickable
        v-ripple
        v-for="(task, key) in tasks"
        :key="task.id"
      >
        <q-item-section>
          <q-item-label overline>{{key + 1}} - {{task.title}}</q-item-label>
          <q-item-label>{{task.completed ? 'Encerrada' : 'A fazer'}}</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      tasks: [],
      users: [],
      usuarioSelecionado: {
        id: 1,
        name: ''
      }
    }
  },
  methods: {
    listTasks () {
      const url = 'http://jsonplaceholder.typicode.com/todos?userId=' + this.usuarioSelecionado.id
      this.$axios.get(url)
        .then(response => {
          this.tasks = (response.data)
        })
    },
    listUsers () {
      const url = 'http://jsonplaceholder.typicode.com/users'
      this.$axios.get(url)
        .then(response => {
          this.users = (response.data)
        })
    }
  },
  beforeMount () {
    this.listTasks()
    this.listUsers()
  }
}
</script>
