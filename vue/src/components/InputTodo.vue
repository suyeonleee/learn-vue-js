<template>
    <div>
        <h4>할 일 추가</h4>
        <input type="text" v-model="newTodo.title">
        <input type="text" v-model="newTodo.description">
        <button @click="sendData">저장</button>

        <button @click="deleteData">취소</button>
    </div>
</template>

<script>
export default {
    name: 'InputTodo',
    data() {
        return {
            newTodo: {
                'title': '',
                'description': '',
                isDone: false

            }

        }
    },
    methods: {
        sendData() {
            if (this.newTodo.title.trim().length > 3
                && this.newTodo.description.trim().length > 3
            ) {
                const param = { ...this.newTodo }
                this.$emit('new-todo', param);
                this.deleteData();
            } else {
                window.alert('형식에 맞는 데이터를 입력해주세요');
            }
        },
        deleteData() {
            this.newTodo.title = '';
            this.newTodo.description = '';
        }
    }
}

</script>
<style scoped></style>