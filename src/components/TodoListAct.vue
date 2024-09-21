<template>
    <v-container class=" mt-12">
      <v-row justify="center">
        <v-col cols="12" md="8">

            <v-card class="pa-4">
            <v-card-title >
              <h3 class="display-1">To-do Notes</h3>
            </v-card-title>

            <v-form @submit.prevent="addTask">
              <v-text-field
                v-model="newTask"
                label="New Task"
                outlined
                dense
                class="mt-4 mb-4"
                append-icon="mdi-plus"
              ></v-text-field>
            </v-form>

            <v-list>
              <v-list-item-group v-for="task in tasks" :key="task.id">
                <v-list-item>
                  <v-row class="align-center w-100 mb-4">
                    <!-- Check Button -->
                    <v-col cols="1">
                      <v-icon
                        @click="toggleCompletion(task.id)"
                        :color="task.completed ? 'green' : 'grey'"
                      >
                        mdi-check-circle
                      </v-icon>
                    </v-col>

                    <v-col cols="9">
                      <v-list-item-content>
                        <v-list-item-title
                          :class="{ 'text--line-through': task.completed }"
                        >
                          {{ task.title }}
                        </v-list-item-title>
                      </v-list-item-content>
                    </v-col>

                    <v-col cols="1">
                      <v-icon @click="removeTask(task.id)" color="red">mdi-delete</v-icon>
                    </v-col>
                  </v-row>
                </v-list-item>
              </v-list-item-group>
            </v-list>
         
        <v-row justify="center">
             <v-col cols="4" class="mr-6">
                 <v-btn @click="clearCompleted" class="ma-0" color="blue" block>
                      Clear Finished Task
                 </v-btn>
             </v-col>
        <v-col cols="4" class="ml-1">
                  <v-btn @click="clearAll" class="ma-0" color="grey" block>
                     Delete All Task
                  </v-btn>
            </v-col>
        </v-row>

            <v-divider></v-divider>
            <v-row justify="end">
              <v-col cols="auto">
                <v-chip class=" ma-6 mb-4">
                  Pending Tasks: {{ pendingTasksCount }}
                </v-chip>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    name: 'TodolistAct',
    data() {
      return {
        newTask: '',
        tasks: [],
      };
    },
    computed: {
      pendingTasksCount() {
        return this.tasks.filter(task => !task.completed).length;
      },
    },
    methods: {
      addTask() {
        if (this.newTask.trim() === '') return;
        this.tasks.push({
          id: Date.now(),
          title: this.newTask.trim(),
          completed: false,
        });
        this.newTask = '';
      },
      toggleCompletion(taskId) {
        const task = this.tasks.find(task => task.id === taskId);
        if (task) task.completed = !task.completed;
      },
      removeTask(taskId) {
        this.tasks = this.tasks.filter(task => task.id !== taskId);
      },
      clearCompleted() {
        this.tasks = this.tasks.filter(task => !task.completed);
      },
      clearAll() {
        this.tasks = [];
      },
    },
  };
  </script>
  
  <style scoped>
  .text--line-through {
    text-decoration: line-through;
  }
  </style>