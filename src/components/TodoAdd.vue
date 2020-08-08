<template>
  <div id="app">
    <v-app id="inspire">
      <v-form method="post" @submit.prevent="postNow">
        <v-container>
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field v-model="task" label="Input Task" required></v-text-field>
            </v-col>
            <v-col cols="12" md="4">
              <v-btn color="success" class="mr-4" type="submit">Add</v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </v-app>
  </div>
</template>

<script>
export default {
  name: "TodoAdd",
  data: () => ({
    task: "Going to ....",
  }),
  methods: {
    postNow(e) {
      e.preventDefault();
      let formData = new FormData();
      formData.set("task", this.task);
      this.axios
        .post("http://localhost:8000/api/v1/todos", formData, {
          headers: {
            "Content-type": "application/json",
          },
        })
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          let { response } = error;
          console.log(response);
        });

      window.location.reload();
    },
  },
};
</script>

<style>
</style>