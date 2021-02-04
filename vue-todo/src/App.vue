<template>
    <div id="app">
        <todo-header></todo-header>
        <todo-input @addTodoItem="addOneItem"></todo-input>
        <todo-list :propsdata="todoItems" 
                @removeTodo="removeOneItem" 
                @toggleItem="toggleOneItem">
        </todo-list>
        <todo-footer @clearAll="clearAllItems"></todo-footer>
    </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
    components: {
        'todo-header' : TodoHeader,
        'todo-input' : TodoInput,
        'todo-list' : TodoList,
        'todo-footer' : TodoFooter,
    },
    data(){
        return{
            todoItems : []
        }
    },
    methods: {
        addOneItem (todoItem){
            var obj = { completed: false, item: todoItem };
            localStorage.setItem(todoItem,JSON.stringify(obj));
            this.todoItems.push(obj);
        },
        removeOneItem (todoItem, index) {
            localStorage.removeItem(todoItem);
            this.todoItems.splice(index, 1);
        },
        toggleOneItem (todoItem,index){
            this.todoItems[index].completed = !this.todoItems[index].completed;
            localStorage.removeItem(todoItem.item);
            localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
        },
        clearAllItems (){
            localStorage.clear();
            this.todoItems = [];
        }
    },
    created(){
        if (localStorage.length > 0){
            for (var i = 0; i < localStorage.length ; i ++){
                if(localStorage.key(i) !== 'loglevel:webpack-dev-server'){
                    this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
                }
            }
        }
    }
}
</script>

<style>
  body{
    text-align: center;
    background-color: #F6F6F6;
  }
  input {
    border-style : groove;
    width: 200px;
  }
  button {
    border-style : groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>