<template>
  <v-container class="fill-height">
    <v-row class="d-flex justify-center align-center">
        <!-- <v-card>
          <p> Perguntados </p>
        </v-card> -->

      <p class="mt-5 titulo"> Perguntecos</p>

      <v-col cols="12" class="d-flex justify-center perguntas">
        <v-card class="pa-6 card">
          <p class="titulo-pergunta" > 1 - Considere o código Python 2.7 a seguir </p>
          <br>
          <p>L=[6,5,4,3,2,1]</p>
          <p>for k in range(-3,3):</p>
          <p> print L[k]</p>
          <br>
          <p>A execução desse código exibe os números:</p>

          <v-radio-group  class="respostas mt-2" row>
              <v-radio class="my-0" label="1 1 1 6 5 4" value="a" />
              <v-radio class="my-0" label="1 2 3 4 5 6;" value="b" />
              <!-- c é a correta -->
              <v-radio class="my-0" label=" 3 2 1 6 5 4;" value="certo" />
              <v-radio class="my-0" label="6 5 4 3 2 1;" value="d" />
              <v-radio class="my-0" label=" 6 5 4 6 5 4;" value="e" />
            </v-radio-group>
        </v-card>
      </v-col>

      <v-col cols="12" class="d-flex justify-center perguntas">
        <v-card class="pa-6 card">
        <p class="titulo-pergunta" > 2 -Analise o código Python a seguir: </p>
        <br>
        <p> x = [1,2,3,4,5,6] x = x[:-1] for i in range(6):      x.append(i) y = x[-1]*x[1]**x[7]%x[9] print(y) </p>
        <br>
        <p> A opção que indica a saída produzida pela execução desse código é:</p>
          <v-radio-group  class="respostas mt-2" row>
              <v-radio class="my-0" label="5" value="a" />
              <v-radio class="my-0" label="3" value="b" />
              <v-radio class="my-0" label="2" value="certo" />
              <v-radio class="my-0" label="1" value="d" />
              <v-radio class="my-0" label="0" value="e" />
          </v-radio-group>
        </v-card>
      </v-col>
      <v-btn class="envio" @click="envio"> ENVIAR </v-btn>

      <!-- <v-col cols="12" class="d-flex justify-center perguntas">
        <v-card class="pa-6 card">
        <p class="titulo-pergunta" > 3 - Quanto é 3 + 3? </p>
          <v-radio-group  class="ma-0 respostas" row>
            <div class="d-flex mt-2">
              <v-radio class="my-0" label="6" value="um" />
              <v-radio class="my-0" label="9" value="dois" />
            </div>
          </v-radio-group>
        </v-card> -->
      <!-- </v-col>  -->
      <task-form :form-label="'Nova Pergunta'" @new-task="addNewTask" class="nova-pergunta"/>
      <v-col v-for="item in items" :key="item.id" cols="12">
        <task :task="item" />
      </v-col> 
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
        this.appStore.showSnackbar(`Nova pergunta adicionada #${task.id}`)
        this.getTasks()
        this.loading = false
        console.log("oi")
      })
    },
    envio(){
      this.loading = true
      if (respostas === certo)
        return this.appStore.showSnackbar("Você acertou a questão 1", "danger")
      else
        return this.appStore.showSnackbar("Poxa você errou a questão 1", "danger")
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
  width: 35rem;
}
.titulo-pergunta{
  text-align: center;
}
.envio{
  color: aliceblue;;
  background-color:  rgb(255, 0, 111);
  padding: 0.5rem ;
  width: 35rem;
  margin-bottom: 1rem;
}
.nova-pergunta{
  width: 19rem;
  margin-left: 2rem;
  height: 8rem;
}
</style>
