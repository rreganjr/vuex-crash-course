<template>
    <div>
        <h3>Todos</h3>
        <div class="legend">
            <span><span class="incomplete-box"></span> = Incomplete</span>
            <span><span class="complete-box"></span> = Complete</span>
            <span class="instructions">Double click to mark complete</span>
        </div>            
        <div class="todos">
            <div @dblclick="onDblClick(todo)" v-bind:class="{'is-complete':todo.completed}" v-for="todo in allTodos" :key="todo.id" class="todo">{{todo.title}} <i @click="deleteTodo(todo.id)" class="fas fa-trash-alt"></i></div>
        </div>
    </div>
</template>

<script>
import { mapGetters, mapActions} from 'vuex';

export default {
    name: "Todos",
    methods: {
        ...mapActions(['fetchTodos', 'deleteTodo', 'updateTodo']),
        onDblClick(todo) {
            const updatedTodo = {
                id: todo.id,
                title: todo.title,
                completed: !todo.completed
            }
            this.updateTodo(updatedTodo);
        }
    },
    computed: mapGetters(['allTodos']),
    created() {
        this.fetchTodos();
    }
}
</script>

<style scoped>
.todos {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
}
.todo {
  border: 1px solid #ccc;
  background: #41b883;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
  position: relative;
  cursor: pointer;
}
.is-complete {
  background: #35495e;

}
 i {
     position: absolute;
     bottom: 10px;
     right: 10px;
     color: #fff;
     cursor: pointer;
 }
 .complete-box {
     margin-left: 30px;
     display: inline-block;
     width: 10px;
     height: 10px;
     background: #35495e;
 }
 .incomplete-box {
     margin-left: 20px;
     display: inline-block;
     width: 10px;
     height: 10px;
     background: #41b883;
 }
 .instructions {
     margin-left: 30px;
 }
 .legend {
     margin-bottom: 1rem;
 }

 @media (max-width: 500px) {
     .todos {
         grid-template-columns: 1fr;
     }
 }

</style>
