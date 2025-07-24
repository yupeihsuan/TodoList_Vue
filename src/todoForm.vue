<script setup>
    import {ref,onMounted} from "vue";

    let selectedType = ref("");

    let chooseTodoType = function(todoType){
        selectedType.value = todoType;
    };

    let todoText = ref("");

    let emit = defineEmits(['addTodo']);

    // let clicked = ref(false);

    let submit = function(){
        if(!todoText.value.trim() || !selectedType.value) {
            alert("請填寫內容並選擇類別！");
            return;
        }

        //傳出新增的代辦事項
        emit('addTodo',{
            id: Date.now(),
            text: todoText.value,
            type: selectedType.value,
            done: false
        });

        //清空輸入框、類別
        todoText.value = "";
        selectedType.value = "";
    }



</script>


<template>
    
    <div class="inputBox">
        <p>建立代辦事項</p>
        <input type="text" class="textBox" v-model="todoText" placeholder="新增代辦事項">
    </div>

    <p>選擇類別</p>
    <div class="typeBox">
        <div class="btn">
            <button :class="['btnBase',selectedType=='work'?'work':'']" @click="chooseTodoType('work')">工作</button>
            <button :class="['btnBase',selectedType=='school'?'school':'']" @click="chooseTodoType('school')">學校</button>
            <button :class="['btnBase',selectedType=='todo'?'todo':'']" @click="chooseTodoType('todo')">提醒</button>
            <button :class="['btnBase',selectedType=='other'?'other':'']" @click="chooseTodoType('other')">其他</button>
        </div>
    </div>

    <div class="submitBox">
        <button @click="submit" class="submitBtn">新增 +</button>
    </div>
    
</template>

<style scoped>
    .textBox{
        padding: 20px 25px;
        width: 500px;
        border-radius: 10px;
        border: solid 1px #ddd;
        color: #666;
        font-size: 16px;
    }

    .inputBox{
        margin-bottom: 25px;
    }

    .typeBox {
        display: flex;
        justify-content: center;
        margin-top: 10px;
        margin-bottom: 25px;
    }

    .btn {
        display: flex;
        gap: 15px;
    }

    .btnBase{
        padding: 10px 10px;
        height: 50px;
        width: 125px;

        border-radius: 10px;
        border: solid 1px #ddd;
        color: #444;
        background-color: #fff;
        font-size: 16px;

        cursor: pointer;
        opacity: 0.85;
        transition: 0.3s;
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

    .btnBase:hover {
        opacity: 0.9;
        transform: translateY(-2px);
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .submitBtn{
        background-color: #6FCF97;
        color: #fff;
        font-size: 16px;
        padding: 10px 10px;
        border: solid 1px #ddd;
        border-radius: 10px;
        cursor: pointer;
        width: 550px;
    }

    .submitBtn:hover {
        background-color: #57B784;
    }

    
    
</style>