<template>
    <div>
        <label for="entire">
            <input type="radio" 
                name="lists" 
                id="entire" 
                value="entire" 
                @change="selectedList"
            >전체 할 일
        </label>
        <label for="completed">
            <input type="radio" name="lists" id="completed" value="completed"
                @change="selectedList"
            >완료된 할 일
        </label>

        <div id="total-list" v-bind="total">전체 개수 : {{ todoList.length }}개</div>

        <ul v-show="selected">
            <li v-for="(todo, index) in todoList" :key="todo.id">
                <span :class="{ todoCompleted: todo.isDone}">
                    제목: {{ todo.title }} / 내용: {{ todo.description }}
                </span>
                <button 
                    @click="completeTodo(todo)"
                >완료</button>
                <button @click="removeTodo(todo, index)">삭제</button>
            </li>
            
        </ul>
        <ul 
            v-show="selected"
            v-if="todoList.isDone"
        >
            <li v-for="todo in todoList" :key="todo.id">
                제목: {{  }} / 내용: {{ }}
            </li>
        </ul>
        <div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ShowList',
    data() {
        return {
            todoList: [],
            total: {
                type: Number
            },
            selected: true,
            obj: {}
        }
    },
    props: {
        showTodo: {
            type:Array,
            default: function() {
                return []
            }
        }
    },
    watch: {
        showTodo: {
            deep: true,
            immediate: true,
            handler() {
            this.todoList = this.showTodo;
              console.log('로드됨, 혹은 변화 감지됨',this.todoList);
            }
        }
        
    },
    computed: {

    },
    methods: {
        selectedList($event) {
            console.log('이거걸랑요', $event.target.value);
        },
        removeTodo(todo, index) {
            this.todoList.splice(index, 1);
        },
        completeTodo(todo){
            todo.isDone = true;
            this.$emit('update-todo', todo);
            
        }
    }
}
</script>
<style scoped>
#total-list {
    text-align: right;
}
.todoCompleted{
    text-decoration:line-through 
}
</style>