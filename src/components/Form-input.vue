<template>
    <div class="control has-icons-left has-icons-right is-block m-auto">
        <div class="is-flex">
            <input v-model="task"  class="input is-rounded is-success" type="text" placeholder="ToDo">
            <button @click="$emit('add', task), clearTask()" class="button is-rounded is-warning ml-1 px-5">+</button>
        </div>
        <span class="icon is-small is-left px-auto">
            <i class="fas fa-tasks"></i>
        </span>
    </div>
</template>

<script>
export default {
    name: "FormInput",
    emits: ['add'],
    data(){
        return{
            task: ""
        }
    },
    methods: {
        clearTask(){
            this.task = ''
        }
    }
}
</script>

<style scoped>
    .control{
        width: 50%;  
    }
    @media screen and (max-width: 500px) {
    .control{
        width: 90%;  
    }
} 
</style>