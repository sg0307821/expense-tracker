<template>
<div class="search-filter-container">
      <input
        type="text"
        v-model="searchQuery"
        placeholder="Search expenses..."
        class="search-input"
      />
      <label>
        From:
        <input type="date" v-model="startDate" class="date-input" />
      </label>
      <label>
        To:
        <input type="date" v-model="endDate" class="date-input" />
      </label>
      <label>
        Min Price:
        <input
          type="number"
          v-model.number="minPrice"
          placeholder="Min"
          class="price-input"
        />
      </label>
      <label>
        Max Price:
        <input
          type="number"
          v-model.number="maxPrice"
          placeholder="Max"
          class="price-input"
        />
      </label>
    </div>
  
  <div>

    <!-- Incompleted Tasks  -->
    <h3 v-if="inCompleteTasks.length > 0" class="status_info">Expenses</h3>
    <div class="tasks" v-for="task in inCompleteTasks" v-bind:key="task.id">
      <Task v-bind:task="task" v-bind:completed="false" />
    </div>



    <!-- Completed Tasks -->
    <h3 v-if="completedTasks.length > 0" class=" completed status_info">Completed</h3>
    <div class="tasks" v-for="task in completedTasks" v-bind:key="task.id">
      <Task v-bind:task="task" v-bind:completed="true" />
    </div>
  </div>
</template>

<script>
import Task from "./Task.vue";
export default {
  name: "TasksComponent",
  props: {
    completedTasks: Array,
    inCompleteTasks: Array,
  },
  components: {
    Task,
  },
};
</script>

<style scoped>
.status_info {
  text-align: center;
  margin-top: 25px;
  color: #111111;
}

.completed {
  border-top: 2px solid grey;
  opacity: 0.3;
}
.search-filter-container {
  display: flex;
  flex-wrap: wrap; /* Allow elements to wrap if needed */
  gap: 10px; /* Add spacing between elements */
  margin-bottom: 20px; /* Add spacing below the filter section */
  align-items: center; /* Vertically align items */
  justify-content: space-between; /* Spread items across the container */
}

.search-input,
.price-input,
.date-input {
  padding: 6px;
  font-size: 0.9rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  flex: 1 0 150px; /* Flexible width with a minimum */
  max-width: 200px; /* Maximum width for inputs */
}

.search-input {
  flex-grow: 2; /* Make search input slightly larger */
}

label {
  font-size: 0.9rem;
  margin-right: 5px;
}
button {
  padding: 8px 12px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
