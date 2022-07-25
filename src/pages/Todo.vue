<template>
    <q-page class="bg-grey-3 column">
        <div class="row q-pa-sm bg-primary">
            <q-input
                @keyup.enter="addTask"
                square
                class="col"
                v-model="newTask"
                placeholder="Add Task"
                dense
                bg-color="white"
            >
                <template v-slot:append>
                    <q-btn @click="addTask" round dense flat icon="add" />
                </template>
            </q-input>
        </div>
        <q-list class="bg-white" separator bordered>
            <q-item
                v-for="(task, index) in tasks"
                :key="task.title"
                tag="label"
                v-ripple
                clickable
                :class="{ 'done bg-green-1': task.done }"
            >
                <q-item-section avatar>
                    <q-checkbox
                        v-model="task.done"
                        class="no-pointer-events"
                        color="primary"
                    />
                </q-item-section>
                <q-item-section>
                    <q-item-label>{{
                        task.title
                    }}</q-item-label> </q-item-section
                ><q-item-section v-if="task.done" side
                    ><q-btn
                        @click.stop="deleteTask(index)"
                        flat
                        round
                        dense
                        color="primary"
                        icon="delete"
                    />
                </q-item-section>
            </q-item>
        </q-list>
        <Transition>
            <div v-if="!tasks.length" class="no-tasks absolute-center">
                <q-icon name="check" size="100px" color="primary"></q-icon>
                <div class="text-h5 text-primary text-center">No tasks</div>
            </div>
        </Transition>
    </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
    data() {
        return {
            newTask: "",
            tasks: [],
        };
    },
    methods: {
        deleteTask(index) {
            this.$q
                .dialog({
                    title: "Confirm",
                    message: "Are you sure you want to delete?",
                    cancel: true,
                    persistent: true,
                })
                .onOk(() => {
                    console.log(">>>> OK");
                    this.tasks.splice(index, 1);
                    this.$q.notify("Task Deleted");
                })

                .onCancel(() => {
                    // console.log('>>>> Cancel')
                    return;
                });
        },
        addTask() {
            console.log("ok");
            this.tasks.push({
                title: this.newTask,
                done: false,
            });
            this.newTask = "";
        },
    },
});
</script>

<style lang="scss">
.done {
    .q-item__label {
        text-decoration: line-through;
        color: #bbb;
    }
}
.no-tasks {
    opacity: 0.5;
}
/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
    transition: opacity 1.5s ease;
}

.v-enter-from,
.v-leave-to {
    opacity: 0;
}
</style>
