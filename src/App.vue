<script>
export default {
    data() {
        return {
            name: 'Saad',
            status: true,
            tasks: [
                { id: 1, title: 'Task One', completed: false },
                { id: 2, title: 'Task Two', completed: true },
                { id: 3, title: 'Task Three', completed: false },
                { id: 4, title: 'Task Four', completed: true },
            ],
            link: 'https://www.google.com',
        };
    },
    methods: {
        toggleStatus() {
            this.status = !this.status;
        }
    }
}
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
            {{ task.title }} - {{ task.completed }}
        </li>
    </ul>
    <br>
    <br>
    <a v-bind:href="link">Google</a>
</template>