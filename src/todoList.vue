<script setup>
    import {ref} from 'vue';

    let props = defineProps(["todos"]);
    let emit = defineEmits(['toggle_done','delete_todo']);

</script>

<template>

    <section class="listBox">

        <div v-for="contents in props.todos" :key="contents.id" :class="['todoItem',{done: contents.done}]">
            <label class="itemBox">
                <input type="checkbox" :checked="contents.done" @change="emit('toggle_done',contents.id)">
                <span class="todoItem_text">{{ contents.text }}</span>
                <span class="label" :class="contents.type">{{ contents.type }}</span>
            </label>

            <button class="deleteBtn" @click="emit('delete_todo',contents.id)">X</button>
        </div>

        <div v-if="props.todos.length==0" class="empty">沒有項目</div>

    </section>
    
</template>

<style scoped>

    .listBox{
        width: 508px;
        /* height: 600px; */
        border: solid 1px #ddd;
        border-radius: 10px;
        background-color: #fff;
        padding: 15px 20px;
    }

    .todoItem{
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px;
        border: solid 1px #eee;
        border-radius: 8px;
        margin-bottom: 10px;
    }

    .todoItem.done span:first-of-type{
        text-decoration: line-through;
        color: #aaa;
    }
    
    .itemBox{
        display: flex;
        align-items: center;
        gap: 10px;
        cursor: pointer;
    }

    .label{
        padding: 5px 10px;
        font-size: 12px;
        border-radius: 12px;
        color: #fff;
    }
    
    .work{
        background-color: #EFCCFF;
        color: #7A0099;
    }

    .school{
        background-color: #CCE0FF;
        color: #003D99;
    }

    .todo{
        background-color: #FFD699;
        color: #A66300;
    }

    .other{
        background-color: #ddd;
        color: #666;
    }

    .deleteBtn{
        border: none;
        background: none;
        color: #d9534f;
        cursor: pointer;
    }

    .empty{
        text-align: center;
        color: #aaa;
    }
    
    

</style>