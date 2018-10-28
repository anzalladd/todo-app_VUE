<template>
    <div>
        <!-- Input Data -->
        <input type="text" placeholder="Apa yang akan anda kerjakan ??" 
        class="todo-input" v-model="newTodo"
        @keyup.enter="addTodo"
        >
        <!-- Output dari Input -->
        <div v-for="(todo, index) in todos" :key="todo.id"  class="todo-item">
            <div class="todo-item-left">
                <!-- double klik to edit -->
                <div class="todo-item-label" v-if="!todo.editing" 
                @dblclick="editTodo(todo)"
                 >
                    {{todo.title}}
                </div>
                <!-- edit input -->
            <input type="text" v-model="todo.title" class="todo-item-edit"
            v-else
            @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" v-focus
            > 
            </div>
            <!-- Remove Item -->
            <div class="remove-item" @click="removeTodo(index)">
            &times;
        </div>
        </div>
    </div>
</template>
s
<script>
export default {
    name:'TodoList',
    data(){
        return{
        newTodo:'',
        idForTodo: 3,
        todos:[
            {
                'id':1,
                'title':'Makan Indomie',
                'completed': false,
                'editing': false,
            },
            {
                'id':2,
                'title':'Makan Sarimie',
                'completed': false,
                'editing': false,
            },
        ]
        }
   },
    directives:{
        focus:{
            inserted: function(el){
                el.focus()
            }
        }
    },
   methods:{
    // Function untuk ngepush data
       addTodo(){
           if (this.newTodo.trim().length == 0) {
               return
           }
           this.todos.push({
               id: this.idForTodo,
               title: this.newTodo,
               completed: false,
               editing: false
           })
           this.idForTodo++,
           this.newTodo = ''


       },
       removeTodo(index){
           this.todos.splice(index,1)
       },
       editTodo(todo){
           todo.editing = true
       },
       doneEdit(todo){
           todo.editing = false
       }
   }

}
</script>

<style lang="scss">
    
.todo-input{
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 12px;

    &:focus{
        outline: 0,
    }
}
.todo-item{
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.remove-item{
    cursor: pointer;
    margin-left: 14px;
    &:hover{
        color: red;
    }
}
.todo-item-left{
    display: flex;
    align-items: center;
}
.todo-item-edit{
    font-size: 24px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    font-family: 'Avenir', Arial, Helvetica, sans-serif;
    &:focus{
        outline: none;
    }
}
</style>

