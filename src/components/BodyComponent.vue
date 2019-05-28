<template>
    <div class="todo_body">
        <form @submit.prevent="addTodo">
            <input autocomplete="off" type="text" v-validate="'min:5'" name="todoName" v-model="todo" placeholder="What are you planning to do?">
        </form>
        <div name="list" class="listTodos">
            <transition-group enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
                <div class="todo_e" v-for="(data, index) in todos" :key="index" v-bind:class="{complete: data.completed}">
                    {{ data.todo }}

                    <a href="javascript:void(0)" @click="data.completed = !data.completed">
                        <i class="fa fa-check-circle" v-if="data.completed === false"></i>
                        <i class="fa fa-window-close" v-if="data.completed === true"></i>
                    </a>
                </div>
            </transition-group>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            todo: '',
            todos: []
        }
    },
    methods: {
        addTodo() {
            this.$validator.validateAll().then((result) => {
                if(result) {
                    this.todos.push({
                        todo : this.todo,
                        completed : false    
                    });
                    this.todo = '';
                }
                else {
                    console.log('Not Valid');
                }
            })
        }
    },
    computed: {
        completeClass() {
            this.classComplete = !this.classComplete;
        }
    }
}
</script>
<style scoped>
    @import url("https://cdn.jsdelivr.net/npm/animate.css@3.5.1");
    @import url("https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css");

    .todo_body {
        margin-top: 30px;
        background: #fff;
        border-radius: 3px;
        box-shadow: 0 0 15px rgba(0,0,0,0.02);
        padding: 15px;
        overflow: hidden;
    }
    input {
        width: 100%;
        box-shadow: none;
        height: 42px;
        border-radius: 0px;
        border: none;
            border-bottom-color: currentcolor;
            border-bottom-style: none;
            border-bottom-width: medium;
        border-bottom: 1px solid #ccc;
        color: #333;
        padding: 0 5px;
    }
    .todo_e {
        background: #f0f0f0;
        color: #333;
        font-size: 14px;
        padding: 15px 5px;
        border-bottom: 1px dashed #ccc;
        display: flex;
        align-items: center;
        justify-content: space-between;
        position: relative;
        user-select: none;
    }
    .todo_e:nth-child(even) {
        background-color: #fff;
    }
    .todo_e:after {
        position: absolute;
        left: 5px;
        right: 40px;
        bottom: 0;
        opacity: 0;
        background-color: #333;
        transition: all ease 0.4s;
        content: '';
        height: 2px;
        margin-bottom: -2px;
    }
    .todo_e a {
        display: inline-flex;
        font-size: 18px;
        color: #f27474;
        border-radius: 50%;
        width: 20px;
        height: 20px;
        align-items: center;
        justify-content: center;
        text-decoration: none !important;
    }
    .todo_e.complete {
        background: #d3f5d3;
        pointer-events: none;
    }
    .todo_e.complete a {
        pointer-events: all;
    }
    .todo_e.complete:after{
        bottom: 50%;
        opacity: 1;
    }
    .todo_e.complete a {
        color: #333;
    }
    .todo_e a:hover {
        color: #333;
    }
    .todo_e.complete a:hover {
        color: #f27474;
    }
</style>

