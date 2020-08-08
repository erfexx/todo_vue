<template>
  <div id="app">
    <v-app id="inspire">
      <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">Task</th>
              <th class="text-left">Is Finished</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in todos" :key="item.name">
              <td>{{ item.task }}</td>
              <td>{{ item.is_finish }}</td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
      <TodoAdd />
    </v-app>
  </div>
</template>

<script>
import TodoAdd from "@/components/TodoAdd.vue";
export default {
  name: "Todo",
  components: {
    TodoAdd,
  },
  created() {
    console.log("get todos data");
    this.axios
      .get("http://localhost:8000/api/v1/todos")
      .then((response) => {
        let { data } = response.data;
        this.todos = data;
        // console.log(data);
      })
      .catch((error) => {
        let { response } = error;
        console.log(response);
      });
  },
  data: () => (
    console.log("first todos data"),
    {
      todos: [],
    }
  ),
};
</script>