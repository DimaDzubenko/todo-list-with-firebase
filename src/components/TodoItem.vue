<template>
    <div>
        <label>{{task.todo}}</label>
        <button @click="deleteTaskItem()">Delete</button>
    </div>
</template>

<script>
export default {
    name: 'TodoItem',

    props:{
        task: {
            type: Object,
            required: true,
            default: null
        }
    },

    methods:{
        deleteTaskItem(){
            console.log(this.task.id);
            this.$emit("deleteTaskToList", `${this.task.id}`); 
        }   
    }
}
</script>

<style scoped>

</style>