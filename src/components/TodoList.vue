<template>
    <div> 
        <div v-for="(task, index) in Tasks" :key="index">
            <TodoItem 
                :task="task"
                @deleteTaskToList="deleteTask"                
            />
        </div> 
    </div>
</template>

<script>
import TodoItem from "@/components/TodoItem.vue";
export default {
    name: 'TodoList',

    components:{
        TodoItem
    },

    props:{
        Tasks:{
            type: Array,
            required: true,
            default: null
        }
    },

    methods:{
        deleteTask(emit){
            console.log(emit);
            this.$emit('deleteTask', emit);
        }
    }
}
</script>

<style scoped>

</style>