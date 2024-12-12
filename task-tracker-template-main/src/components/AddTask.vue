<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Category</label>
      <input type="text" v-model="text" name="text" placeholder="Add Expense" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input type="text" name="day" v-model="day" placeholder="Add Day & Time" />
    </div>
    <div class="form-control">
      <label>Amount</label>
      <input type="text" name="day" v-model="amount" placeholder="Add amount" />
    </div>
    

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>
</template>
<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      amount:"",
      reminder: false,
      completed: false,
    };
  },
  props: {
    userName: String,
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      console.log("New Task Added");

      if (!this.text) {
        alert("Please add a task");
        return;
      }

      const newTask = {
        text: this.text,
        day: this.day,
        amount:this.amount,
        reminder: this.reminder,
        completed: this.completed,
        userName: this.userName,
        createdBy: this.$store.state.userName,
      };

      this.text = "";
      this.day = "";
      this.amount="";
      this.reminder = false;
      this.$store.dispatch("addTask", newTask);
    },
  },
};
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>
