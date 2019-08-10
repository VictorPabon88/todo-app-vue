<template>

    <div class="container mx-auto px-4 py-20 flex flex-col flex-wrap">
        
        <h1 class="font-serif text-6xl text-center text-gray-300">Taskl-¡</h1>


        <todo-card class="bg-teal-900 mx-auto mt-4 h-full w-full max-w-lg">

            <div class="md:flex-2">
              <input type="text"
               class="font-size: 12px font-family: Helvetica flex-6 mx-auto mt-4 w-4/5 h-10 max-w-lg bg-white hover:bg-gray-100 rounded-full bold py-2 px-4 border-b-4 border-gray-600 hover:border-gray-500 rounded input-group-field"
               autofocus autocomplete="off"
               v-model="newTask"
               @keyup.enter="addTask"
               placeholder="New task">
              <button @click="addTask()" class="flex-2 mx-2 bg-green-500 hover:bg-green-400 text-white font-bold py-2 px-4 border-b-4 border-green-700 hover:border-green-500 rounded rounded-full">
                  Add
              </button>

              </div>
        </todo-card>

<h2 class="font-serif text-6xl text-center text-gray-300">L-¡st</h2>

        <div class="shadow-2xl"></div>

        <todo-card class="task-imput bg-gray-300 mx-auto mt-10 w-full  border rounded max-w-lg round"> <div id="app">
  <task-list :tasks="tasks"></task-list>
            <li v-for="task in tasks" :key="task.id" class="task-item">  {{task.title}} </li>
      
  </div>
<div class="remove-item" @click="removeTask(index)">
  &times;

</div>
           </todo-card>
             

         
        
        

        <todo-card class="bg-teal-900 mx-auto mt-10 w-70 max-w-lg">
          
<button class="flex-2 mx-2 bg-gray-500 hover:bg-gray-400 text-white font-bold py-2 px-4 border-b-4 border-gray-700 hover:border-gray-500 rounded">
  Edit
</button>

<button class="flex-2 mx-2 bg-red-500 hover:bg-red-400 text-white font-bold py-2 px-4 border-b-4 border-red-700 hover:border-red-500 rounded">
  Delete all
</button> 

<button @click="clearCompleted(task)" class="flex-2 mx-2 bg-yellow-500 hover:bg-yellow-400 text-white font-bold py-2 px-4 border-b-4 border-yellow-700 hover:border-yellow-500 rounded">
  Task Complete</button>  <transition-group name="fade" tag="ul" class="tasks__list no-bullet">
          <task-item v-for="(task, index) in tasks"
                     @remove="removeTask(index)"
                     @complete="completeTask(task)"
                     :task="task"
                     :key="task"></task-item>
                     </transition-group>

        </todo-card>
        
        </div>
    

</template>


<script>
export default {

    data () {
        return {
            newTask: '',
            idForTask: 3,
            tasks: [
          {
            'id':1,
            'tittle': 'blabla',
            'completed': false, 
          },
              {
            'id':2,
            'tittle': 'blabla',
            'completed': false, 
          },
            ]
        };
    },

    mounted () {

    },

    methods: {
  addTask() {
       this.tasks.push({
          id: this.idForTask,
          title: this.newTask,
          completed: false
        })

        this.newTask = '';
        this.idForTask++
        }
    },
removeTask(index){
  this.tasks.splice(index, 1)

},



    completeTask(task) {
      task.completed = ! task.completed;
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(this.inProgress);
    },
    clearAll() {
      this.tasks = [];
    },
  }
;

</script>