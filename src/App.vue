<script setup>
import { ref, onMounted } from 'vue';

const name = ref('John Doe');
const status = ref(true);
const newTask = ref('');

const tasks = ref([
    { id: 1, title: 'Task 1', completed: false },
    { id: 2, title: 'Task 2', completed: true },
    { id: 3, title: 'Task 3', completed: false },
]);
const link = ref('https://www.google.com');
const addTask = () => {
    tasks.value.push({
        id: tasks.value.length + 1,
        title: newTask.value,
        completed: false
    });
    newTask.value = '';
};
const deleteTask = (id) => {
    tasks.value = tasks.value.filter(task => task.id !== id);
};

const toggleStatus = () => {
    status.value = !status.value;
};

onMounted((async () => {
    try {
        const res = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await res.json();
        tasks.value = data; // update tasks
    } catch (error) {
        console.log(error);

    }
    console.log('Component mounted');
}));

</script>
<template>
    <h1>{{ name }}</h1>
    <p v-if="status"> user is active</p>
    <p v-else> user is inactive</p>
    <button @click="toggleStatus">Toggle Status</button>
    <button v-on:click="toggleStatus"> toggle status</button>

    <br>
    <br>
    <h3>tasks</h3>
    <ul>
        <li v-for="task in tasks" :key="task.id">
            <span>
                {{ task.title }} - {{ task.completed }}
            </span>
            <button @click="deleteTask(task.id)">Delete</button>
        </li>
    </ul>
    <br>
    <br>
    <!-- <a v-bind:href="link">Google</a> -->
    <br>
    <br>
    <form @submit.prevent="addTask">
        <label for="newTask"></label>
        <input type="text" id="newTask" v-model="newTask" name="newTask">

        <button type="submit">Add Task</button>
    </form>
</template>