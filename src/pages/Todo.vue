<template>
  <q-page class="bg-grey-3 column">
    <div class="row q-pa-sm bg-secondary">
      <q-input
        @keyup.enter="addTask"
        filled
        class="col q-pa-sm"
        bg-color="white"
        v-model="taskInput"
        label="Add Task"
        placeholder="e.g. Go to the Mall"
        dense
      >
        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="add" />
        </template>
      </q-input>
    </div>
    <q-list class="bg-white" separator bordered>
      <q-item
        clickable
        @click="task.done = !task.done"
        :class="{ 'done bg-blue-1': task.done }"
        v-for="(task, i) in tasks"
        :key="i"
        v-ripple
      >
        <q-item-section avatar>
          <q-checkbox calss="no-pointer-events" v-model="task.done" />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{ task.title }}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn
            @click.stop="deleteTask(i)"
            flat
            round
            color="primary"
            icon="delete"
          />
        </q-item-section>
      </q-item>
    </q-list>
    <div v-if="!tasks.length" class="no-tasks absolute-center">
      <q-icon name="check" size="100px" color="primary"></q-icon>
      <div class="text-h5 text-primary text-center">
        No Tasks
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  data: () => ({
    taskInput: "",
    tasks: [
      {
        title: "Clean Car",
        done: false
      },
      {
        title: "Buy Cleaning Stuff for Car",
        done: false
      },
      {
        title: "Go to Work",
        done: false
      },
      {
        title: "Brush your teeth",
        done: false
      }
    ]
  }),
  methods: {
    deleteTask(index) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Are you sure you want to delete this?",
          cancel: true,
          persistent: true
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          this.$q.notify({ message: "Task deleted", color: "primary" });
        });
    },
    addTask() {
      this.tasks.push({ title: this.taskInput, done: false });
      this.taskInput = "";
    }
  }
};
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
</style>
