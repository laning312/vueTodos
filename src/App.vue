<template>
    <div id="app">
        <h1>{{title}}</h1>
        <ul class="todos">
            <li>
                <input type="text"
                placeholder="快写下您要我记住的事儿吧"
                autofocus="true" @keyup.enter="addItem" v-model="newTodo">
            </li>
            <li v-for="(todo, index) in todos" :class="{'checked': todo.done}">
                <input type="checkbox" v-model="todo.done" @change="saveToStore">
                <label for="">{{index+1}}. {{todo.value}}</label>
                <time>{{todo.created}}</time>
                <button @click="delItem(index)"></button>
            </li>
        </ul>
    </div>
</template>

<script>
    import './assets/site.less';
    import './assets/todos.less';

    export default{
//        name: 'app',
        data() {
            return {
                newTodo: '',
                title: 'vue-todos',
                todos: []
            }
        },

        created() {
            if(localStorage.getItem("vue-todos") != null){
                this.todos = JSON.parse(localStorage.getItem("vue-todos"));
            }

        },

        methods: {
            addItem() {
                this.todos.push({
                    value: this.newTodo,
                    created: new Date().toLocaleString(),
                    done: false
                });
                this.saveToStore();
                this.newTodo = '';
            },

            delItem(index) {
                this.todos.splice(index, 1);
                this.saveToStore();
            },

            saveToStore() {
                localStorage.setItem("vue-todos", JSON.stringify(this.todos));
            }
        }
    }
</script>

<style>
    
</style>