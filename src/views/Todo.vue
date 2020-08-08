<template>
  <div id="app">
    <v-app id="inspire">
      <v-simple-table>
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left">Task</th>
              <th class="text-left">Finish ??</th>
              <th class="text-left"></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in todos" :key="item.name">
              <td>
                <h3 class="strike" v-if="item.is_finish == 1">{{ item.task }}</h3>
                <h3 v-else>{{ item.task }}</h3>
              </td>
              <td>
                <v-checkbox
                  input-value="false"
                  v-if="item.is_finish == 0"
                  v-model="item.is_finish"
                  @change="setUpdate(item.id, item.task, item.is_finish)"
                ></v-checkbox>
                <v-checkbox
                  input-value="true"
                  v-else
                  v-model="item.is_finish"
                  @change="setUpdate(item.id, item.task, item.is_finish)"
                ></v-checkbox>
              </td>
              <td>
                <v-btn small color="error" @click="deleteTask(item.id)">
                  <v-icon small>mdi-delete</v-icon>
                </v-btn>
              </td>
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
  methods: {
    setUpdate: function (id, task, status) {
      this.axios
        .patch(
          "http://localhost:8000/api/v1/todos/" + id,
          { task: task, is_finish: status },
          {
            headers: {
              "Content-type": "application/json",
            },
          }
        )
        .then((response) => {
          console.log(response);
          window.location.reload();
        })
        .catch((error) => {
          let { response } = error;
          console.log(response);
        });
    },
    deleteTask: function (id) {
      console.log(id);
      this.axios
        .delete("http://localhost:8000/api/v1/todos/" + id, {
          headers: {
            "Content-type": "application/json",
          },
        })
        .then((response) => {
          console.log(response);
            window.location.reload();
        })
        .catch((error) => {
          let { response } = error;
          console.log(response);
        });
    },
  },
};
</script>

<style>
.strike {
  text-decoration: line-through;
  color: grey;
}
</style>