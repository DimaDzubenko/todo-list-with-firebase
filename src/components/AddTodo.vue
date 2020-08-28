<template>
    <div>  
        <h1>TO-DO List</h1>         
        <input             
            type="text" 
            placeholder="Enter your task"
            v-model="todo"            
        >   
        <button 
            type="button"   
            v-if="Tasks.length < 10"           
            @click="conservedTodo()"                           
        >
            Save
        </button>       
    </div>
</template>

<script>
export default {
    name: 'AddTodo',
    data(){
        return{
            todo: ''
        }
    },

    props:{
        Tasks:{
            type: Array,
            required: true,
            default: null
        }
    },

    methods:{
        conservedTodo(){
            this.$emit('conservedTask', this.todo);
        }
    }
}
</script>

<style>

</style>