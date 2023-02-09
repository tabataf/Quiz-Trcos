<template>
  <v-container class="fill-height">
    <v-row class="d-flex justify-center align-center">
        <!-- <v-card>
          <p> Perguntados </p>
        </v-card> -->

      <p class="mt-5 titulo"> Perguntecos</p>

      <v-col cols="12" class="d-flex justify-center perguntas">
        <v-card class="pa-6 card">
          <p class="titulo-pergunta" > 2 - O que é Machine Learnin? </p>
          <v-radio-group  class="respostas mt-2" row>
              <v-radio class="my-0" label="2" value="um" />
              <v-radio class="my-0" label="4" value="dois" />
              <v-radio class="my-0" label="A sua é minha" value="tres" />
              <v-radio class="my-0" label="7" value="quatro" />
            </v-radio-group>
        </v-card>
      </v-col>

      <v-col cols="12" class="d-flex justify-center perguntas">
        <v-card class="pa-6 card">
        <p class="titulo-pergunta" > 2 - O que é Machine Learnin? </p>
          <v-radio-group  class="respostas mt-2" row>
              <v-radio class="my-0" label="2" value="um" />
              <v-radio class="my-0" label="4" value="dois" />
              <v-radio class="my-0" label="A sua é minha" value="tres" />
              <v-radio class="my-0" label="7" value="quatro" />
          </v-radio-group>
        </v-card>
      </v-col>

      <!-- <v-col cols="12" class="d-flex justify-center perguntas">
        <v-card class="pa-6 card">
        <p class="titulo-pergunta" > 3 - Quanto é 3 + 3? </p>
          <v-radio-group  class="ma-0 respostas" row>
            <div class="d-flex mt-2">
              <v-radio class="my-0" label="6" value="um" />
              <v-radio class="my-0" label="9" value="dois" />
            </div>
          </v-radio-group>
        </v-card>
      </v-col> -->
      <!-- <task-form :form-label="'Nova Tarefa'" @new-task="addNewTask" /> -->
      <!-- <v-col v-for="item in items" :key="item.id" cols="12">
        <task :task="item" />
      </v-col> -->
    </v-row>
  </v-container>
</template>

<script>
import { useAppStore } from "@/stores/appStore"
import TasksApi from "@/api/tasks.api.js"
import Task from "@/components/Task.vue"
import TaskForm from "@/components/TaskForm.vue"

export default {
  name: "TasksList",
  components: { Task, TaskForm },
  setup() {
    const appStore = useAppStore()
    return { appStore }
  },
  data() {
    return {
      loading: false,
      items: [],
    }
  },
  mounted() {
    this.getTasks()
  },
  methods: {
    getTasks() {
      this.loading = true
      TasksApi.getTasks().then((data) => {
        this.items = data.todos
        this.loading = false
      })
    },
    addNewTask(task) {
      this.loading = true
      TasksApi.addNewTask(task.title).then((task) => {
        this.appStore.showSnackbar(`Nova tarefa adicionada #${task.id}`)
        this.getTasks()
        this.loading = false
        console.log("oi")
      })
    },
  },
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=Righteous&display=swap');
  @import url('https://fonts.googleapis.com/css2?family=Lato&display=swap');
.done {
  text-decoration: line-through;
}
.headline{
  color: rgb(255, 0, 111);
}
.respostas{
  display: flex;
  align-items: center;
}
.titulo {
  font-size: 3rem;
  color: rgb(255, 0, 111);
  font-family: 'Righteous', cursive;
}
.perguntas{
  font-family: 'Lato', sans-serif;
  font-size: 1.3rem;
}
.card {
  width: 25rem;
}
.titulo-pergunta{
  text-align: center;
}
</style>
