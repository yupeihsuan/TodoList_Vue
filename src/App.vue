<script setup>
    import {ref,computed,onMounted,watch} from "vue";
    import todoForm from "./todoForm.vue";
    import todoList from "./todoList.vue";

    let todos = ref([]);

    //localstorage
    onMounted(() => {
        let saved = localStorage.getItem("todos");
        if (saved) {
            todos.value = JSON.parse(saved);
        }
    });


    watch(todos, (newVal) => {
        localStorage.setItem("todos", JSON.stringify(newVal));
    }, { deep: true });

    //新增代辦事項
    let addTodo = function (newTodo){
        todos.value.push(newTodo);
    }

    let activeTab = ref('all');

    //切換上方標籤列
    let setTab = function(tab){
        activeTab.value = tab;
    }

    //勾選已完成
    let toggle_done = function(id){
        let todo = todos.value.find(t => t.id == id); //function(t){return t.id==id}
        if(todo){
            todo.done = !todo.done;
        }
    }

    //刪除代辦事項
    let delete_todo = function(id){
        todos.value = todos.value.filter(t => t.id != id);
    }

    // 依照目前篩選標籤計算要顯示的 todos
    const filteredTodos = computed(() => {
    if (activeTab.value === 'todo') {
        return todos.value.filter(t => !t.done);
    } else if (activeTab.value === 'done') {
        return todos.value.filter(t => t.done);
    } else {
        return todos.value;
    }
    });

</script>

<template>
    <section class="box">
        <div class="todoForm">
            <todoForm @addTodo="addTodo"></todoForm>
        </div>

        <div class="headline">
            <p :class="{active:activeTab == 'all'}" @click="setTab('all')">全部</p>
            <p :class="{active:activeTab == 'todo'}" @click="setTab('todo')">待完成</p>
            <p :class="{active:activeTab == 'done' }" @click="setTab('done')">已完成</p>
        </div>

        <div class="todoList">
            <todoList :todos="filteredTodos" @toggle_done="toggle_done" @delete_todo="delete_todo"></todoList>
        </div>
        
    </section>
    
</template>

<style scoped>

    .box{
        max-width: 550px;
        margin: 40px auto;
        color: #888;
    }

    .todoForm{
        margin-bottom: 25px;
    }

    .headline{
        display: flex;
        justify-content: center;
        gap: 50px;
        margin-bottom: 10px;
        cursor: pointer;
        font-weight: 500;
        border-bottom: solid 1px #ddd;
        padding-bottom: 10px;
    }

    .headline p{
        color: #999;
    }

    .headline p.active{
        color: #333;
        border-bottom: solid 3px #6fcf97;
    }

</style>

<style>
    body {
    background-color: #f2f2f2;
    margin: 0;
    }
</style>
