<template>
<div class="todoStyle is-flex is-justify-content-space-around mt-4" >
      <span class="icon-text">
            <span v-if="pressEdit" class="title is-3">
            <strong><input v-model="newTodo" @blur="checkEdit(), changeIcon()" class="input is-rounded is-success" type="text" placeholder="new Todo"></strong>
            </span>         

            <span v-else class="title is-3">
            <strong>{{ msg }}</strong>
            </span>

              <span v-if="!pressEdit" @click.prevent="checkEdit(), changeIcon()" class="icon has-text-info is-block p-1">
                <i class="fas fa-2x fa-pen-square"></i>
              </span> 

               <span v-else @click.prevent="changeIcon()" class="icon has-text-info is-block p-1">
                <i class="fas fa-2x fa-save"></i>
              </span>      
              
              <span  @click="$emit('remove')" class="icon has-text-danger is-block p-1 ml-3">
                <i style="max-width:25px;" class="fas fa-2x fa-trash"></i>
              </span>    
      </span>
</div>
</template>

<script>
export default {
  name: 'To-do',
  emits: ['remove', 'edit'],
  props: {
    msg: {
    type: String,
    required: true,
    default: ""
    },
    selected: Number
  },
  data() {
    return {
      pressEdit: false,
      newTodo: "",
    }
  },
  methods:{
    checkEdit(){
      if(this.newTodo && this.pressEdit){
          this.$emit('edit', this.newTodo, this.selected);
          this.changeIcon()
        }         
    },
    changeIcon(){
      return this.pressEdit = !this.pressEdit
    }
  },
}
</script>

<style scoped>
.todoStyle{
  width: 70%;
  margin: auto;
}
.icon-text{
  flex-wrap: nowrap;
}
.icon:hover{
  cursor: pointer;
} 

    @media screen and (max-width: 550px) {
    .todoStyle{
        width: 85%;  
    }
    .title{
      font-size: 1.8rem;
    }
    .icon-text{
      flex-wrap: nowrap;
    }
}
</style>
