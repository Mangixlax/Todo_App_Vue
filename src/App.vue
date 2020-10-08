<template>
  <div id="app" class="h-100">
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
          
        <div class="row">
          <input v-model="addFormValue" v-on:keydown.enter="addTask" v-on:keydown.esc="clearAddForm" class="form-control form-control-lg" id="addForm" type="text" placeholder="Type to search or enter to add todo">
        </div>

        <div class="row mt-3 mb-5 justify-content-center">
          <button @click="addTask" class="btn btn-lg border text-white" id="addButton">Add</button>
        </div>

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
              <ol class="list-group" id="task_list">              
                <li v-for="(task, index) in tasks" class="list-group-item border-0 mt-0">
                  <div class="row m-0 mb-4">

                    <div class="col-md-10 col-sm-9 pl-2">
                      <div class="custom-control custom-checkbox pt-2 ml-1">
                        <input v-bind:id="`task_${index}`" v-model='task.complete' class="custom-control-input" type="checkbox">
                        <label v-bind:for="`task_${index}`" v-bind:class="{ lineThrough : task.complete }" class="custom-control-label font-weight-bold">
                          {{task.text}}              
                        </label>                
                      </div>                
                    </div>
                  
                    <div class="col-md-2 col-sm-3 text-right pt-1">
                      <button @click="delTask(index)" class="btn btn-md btn-danger deleteBtn">Delete</button>            
                    </div>

                  </div>                   
                  <hr class="">            
                </li>                                       
              </ol> 
            </div>         
          </div>
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      addFormValue: '',
      tasks: [], // создаём массив для записи сюда данных о задаче
      isActive: true,
    }
  },
  methods: { // указываем пользовательские методы для 
    addTask() { // метод для добавления задачи
      this.tasks.push({
       text: this.addFormValue, 
       complete: false,     
      })
      this.addFormValue = '' 
    },
    delTask(index){
      this.$delete(this.tasks, index)
    },
    clearAddForm(){
      this.addFormValue = ""
    }
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
