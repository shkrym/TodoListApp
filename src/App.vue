<template>
  <v-app>
    <!-- Main Navigation (Optional) -->
    <v-app-bar app color="blue">
      <v-toolbar-title>To-Do Notes</v-toolbar-title>
    </v-app-bar>

    <!-- Main Content -->
    <v-main>
      <div style="background-color: #f0f0f0; min-height: 100vh;">
        <v-container>
          <!-- Include the To-Do List Component Here -->
          <TodoListAct />
        </v-container>
      </div>      
    </v-main>
  </v-app>
</template>

<script>
import TodoListAct from './components/TodoListAct.vue';

export default {
  name: 'App',

  components: {
    TodoListAct,
  },

  data: () => ({
    //
  }),
}
</script>
