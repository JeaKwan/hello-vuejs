<template>
  TodoSimpleForm

  <form @submit.prevent="onSubmit">
      <div >
        <input         
          type="text" 
          v-model="todo" 
          placeholder="Type new to-do"
        >  
      </div>
      <div>
        <button          
          type="submit"
        >
        Add
        </button>
      </div> 
      <div v-show="hasError" style="color:red">
        This field cannot be empty
      </div>     
    </form>
</template>

<script>
  import { ref } from 'vue';
  
  export default {
    emits: ['add-todo'],
    setup(props, context) {
        const todo = ref('');
        const hasError = ref(false);
        const onSubmit = () => {
            if (todo.value ==='') {
                hasError.value = true;
            } else{
                emit('add-todo', {
                    id: Date.now(),
                    subject: todo.value,
                    completed: false,
                });
               
            hasError.value = false;
            todo.value = '';
            } 
          }  
       
    
        return {
            todo,
            hasError,
            onSubmit,
       }
      }
    }
</script>

<style>

</style>