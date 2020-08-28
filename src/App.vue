<template>
  <div id="app">
    <div>
      <AddTodo
        @conservedTask="conservedTask($event)"
        :Tasks="tasks"
      />
      <hr>
      <TodoList        
        :Tasks="tasks"
        @deleteTask="deleteTask"
      />      
    </div>     
  </div>
</template>

<script>
import AddTodo from "@/components/AddTodo.vue";
import TodoList from "@/components/TodoList.vue";

export default {
  name: 'App',

  components:{
    AddTodo,
    TodoList
  },

  data(){
    return{
      tasks:[],
      
    }
  },

  beforeMount(){   
    this.$http.get("https://http-my-to-do-list.firebaseio.com/tasks.json")
    .then(responce=>{
      return responce.json()
      })
      .then(responce=>{
        for(let item in responce) { this.tasks.push({...responce[item], id: item });
        // проверка с помощью консоли:
        //console.log('RESPONCE - ' + responce);
        //console.log('ITEM : ' + item);
        //console.log('RESPONCE[ITEM] - ' + responce[item]);
        }
        //==============================================================
        //работа с ответом БД через обьект.
        //Object.values(responce).forEach(item => this.tasks.push(item));
      }
    )   
  },

  methods:{
    // методо добавления таска в БД
    async conservedTask(event){
      let task = {todo: event, status: false};
      try {
        await this.$http.post("https://http-my-to-do-list.firebaseio.com/tasks.json", task).then((responce)=>{
            console.log(responce);            
          });
      } 
      catch(e) {
        console.log(e);
      } 
      finally { 
        // очищаем наши таски.
        this.tasks = []; 
        // делаем новый запрос отображаем полный список. 
        this.$http.get("https://http-my-to-do-list.firebaseio.com/tasks.json").then(responce=>{
          return responce.json();
        }).then(responce=>{
          for(let item in responce) { 
            this.tasks.push({...responce[item], id: item });        
          }        
        })
      }
    },

    //метод удаления таска
    async deleteTask(event){      
      try{
        await this.$http.delete(`https://http-my-to-do-list.firebaseio.com/tasks/${event}.json`);
      } catch(e){
        console.log(e);
      }finally {
        this.tasks = []; 
        this.$http.get("https://http-my-to-do-list.firebaseio.com/tasks.json").then(responce=>{
          return responce.json();
        }).then(responce=>{
          for(let item in responce) { 
            this.tasks.push({...responce[item], id: item });        
          }        
        })
      }
    }  
  }
}
</script>

<style>

</style>