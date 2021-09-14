<template>
  <div class="pa-10">
    <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>

    <v-list two-line subheader class="pt-0">
      <div v-for="item in todo" :key="item.id">
        <v-list-item
          @click="doneTask(item.id)"
          :class="{ 'light-green lighten-4': item.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="item.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': item.done }"
                >{{ item.task }}</v-list-item-title
              >
              <v-list-item-subtitle>{{ item.plus }}</v-list-item-subtitle>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(item.id)">
                <v-icon>mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "Todo",

  components: {},
  data() {
    return {
      newTaskTitle: "",
      todo: [],
    };
  },
  methods: {
    doneTask(id) {
      let item = this.todo.filter((item) => item.id === id)[0];
      item.done = !item.done;
    },
    deleteTask(id) {
      this.todo = this.todo.filter((item) => item.id !== id);
    },
    addTask() {
      let newTask = {
        id: Date.now(),
        task: this.newTaskTitle,
        plus: "",
        don: false,
      };
      this.todo.push(newTask);
    },
  },
};
</script>
