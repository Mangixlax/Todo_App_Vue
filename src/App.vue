<template>
  <div id="todoApp" class="h-100" >
    <div class="container-fluid bg-primary h-25">

      <div class="row justify-content-center h-100">
        <div class="col-md-12 align-self-center ">
          <h1 class="text-center"><a href="#" class="text-white">ToDo App!</a></h1>
          <h6 class="text-center text-white">Add New TO-DO</h6>
        </div>
      </div>

    </div> 
    <div class="container h-100">
        
      <AddTodo
      @addTask="addTask"/>

      <div class="container bg-white h-100 p-0">

        <div class="row  pt-4">
          <div class="col-3 text-right">
            All Todo : <span id="taskCount"> {{ tasks.length }} </span> 
          </div>
          <div class="col-1 text-right offset-1">
            <i class="fas fa-exclamation-circle text-primary"></i>
          </div>
          <div class="col-2 col-md-3 col-sm-3 text-left text-primary pl-0">
            <span id="incompleete">{{ getIncompleteLength }}</span><span> Incomplete</span>
          </div>
          <div class="col-1 col-md text-right">
            <i class="fas fa-check text-success"></i>
          </div>
          <div class="col-2 text-success col-md-3 col-sm-3 pl-0">
           <span id="compleete">{{ getCompleteLength }}</span><span> Completed</span>
          </div>
                              
        </div>

     
        <div class="row">
          <div class="container">
            <hr class="mt-3">
            <Todos
            :tasks="tasks"
            @deleteTask="deleteTask"/>
          </div>         
        </div>
        
      </div>

    </div>

  </div>
</template>

<script>

import AddTodo from "./components/AddTodo.vue";
import Todos from "./components/Todos.vue";

export default {
  name: 'app',
  components: {
    AddTodo,
    Todos
  },
  data () {
    return {      
      tasks: [], // создаём массив для записи сюда данных о задаче
    }
  },
  methods: { // указываем пользовательские методы для 
    addTask(addFormValue) { // метод для добавления задачи
      this.tasks.push({
       text: addFormValue, 
       complete: false,     
      }) 
    },
    deleteTask(index){
      this.$delete(this.tasks, index)
    },
  },
  computed: {
    getIncompleteLength() { 
      return this.tasks.filter((task) => task.complete !== true).length
    },
    getCompleteLength() {
      return this.tasks.length - this.getIncompleteLength
  },
  },
  watch: {
    tasks: {
      deep: true,
      handler(new_tasks_by_aslan) {
        console.table(new_tasks_by_aslan)
      }
    }
  }
}
</script>

<style>

html, body {
  height: 100%; /*чтобы прижать футер к низу*/  
}


hr {
  margin-top: 0;
  margin-bottom: 1;
  border: 0;
  border-top: 1px solid rgba(0, 0, 0, 0.1);
}

.lineThrough {
  text-decoration: line-through;
 
}

</style>
