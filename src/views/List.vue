<template>
    <div>
        <h1>List</h1>
        <hr/>
        <div class="row">
            <div class="input-field s6 col">
                <select ref="select" class="browser-default" v-model="filter">
                    <option value="" disabled selected>Status filter</option>
                    <option value="active">Active</option>
                    <option value="outdated">Outdated</option>
                    <option value="completed">Completed</option>
                </select>
                <br>
                <button v-if="filter" class="btn btn-small red" @click="filter = null">Reset filter</button>
            </div>
        </div>
        <hr>

        <table v-if="tasks.length">
            <thead>
            <tr>
                <th>#</th>
                <th>Title</th>
                <th>Date</th>
                <th>Description</th>
                <th>Status</th>
                <th>Open</th>
            </tr>
            </thead>
            <tbody>
            <tr
                v-for="(task,index) of filterTasks"
                :key="task.id"
            >
                <td>{{ index + 1 }}</td>
                <td>{{ task.title }}</td>
                <td>{{ new Date(task.date).toLocaleDateString() }}</td>
                <td class="width-td">
                    <div class="cutted-text">{{ task.description }}</div>
                </td>
                <td class="active">{{ task.status }}</td>
                <td>
                    <router-link :to="'/task/' + task.id" custom v-slot="{navigate}">
                        <button class="btn btn-small" @click="navigate" @keypress.enter="navigate" role="link">Create
                        </button>
                    </router-link>
                </td>
            </tr>
            </tbody>
        </table>
        <p v-else>No tasks</p>
    </div>
</template>

<script>
import {mapGetters} from 'vuex';

export default {
    data: () => ({
        filter: null
    }),
    computed: {
        ...mapGetters(['tasks']),
        filterTasks() {
            return this.tasks.filter(t => {
                if(!this.filter) {
                    return true;
                } else {
                    return t.status === this.filter
                }

            })
        }
    },
    // methods: {
    //     resetFilter() {
    //         this.filter = false;
    //     }
    // },
    mounted() {
        M.FormSelect.init(this.$refs.select);
    }
}
</script>

<style scoped lang="scss">
.width-td {
    max-width: 400px;
}

.cutted-text {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}
.active {
    color: green;
}
</style>