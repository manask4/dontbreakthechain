<template>
  <div class="container mx-auto w-4/5 md:w-1/2 mb-4">
    <div class="bg-indigo-500 p-6 flex flex-col rounded-md shadow-lg">
      <div v-if="habitStore.length > 0" class="flex flex-wrap mb-4">
        <span
          class="flex items-center mr-2 mb-2 px-3 py-2 text-sm bg-yellow-100 text-gray-700 rounded-full cursor-pointer transition-all shadow-lg"
          v-for="(habit, index) in habitStore"
          :key="index"
          @click="loadHabit(habit)"
        >
          <span>{{ habit }}</span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-edit-3 h-4 w-4 text-gray-600 ml-1"
          >
            <path d="M12 20h9"></path>
            <path
              d="M16.5 3.5a2.121 2.121 0 0 1 3 3L7 19l-4 1 1-4L16.5 3.5z"
            ></path>
          </svg>
        </span>
      </div>
      <div class="self-start text-lg font-bold text-white mb-1">
        <span v-if="prevHabit.length > 0">Edit Habit</span>
        <span v-else>Add Habits to track</span>
      </div>
      <div class="flex">
        <input
          v-model="habits"
          required
          placeholder="Reading, Writing, Exercise, Journaling..."
          class="border h-10 px-4 rounded-md flex-1"
          type="text"
        />
      </div>
      <p
        v-if="prevHabit.length == 0"
        class="text-xs self-start text-gray-200 mt-1"
      >
        Enter single or multiple habits separated by a comma. For eg:
        Reading,Writing,Exercise
      </p>
      <div v-show="!prevHabit" class="mt-2 flex justify-end">
        <button
          class="flex-1 md:flex-none mr-2 bg-indigo-600 text-white p-2 md:px-10 rounded-md mt-4"
          @click="closeDialog"
        >
          Close
        </button>
        <button
          class="flex-1 md:flex-none bg-yellow-400 p-2 md:px-10 text-gray-700 rounded-md mt-4 shadow-lg"
          @click="saveHabits"
        >
          Save
        </button>
      </div>
      <div v-show="prevHabit" class="mt-6 flex justify-end">
        <button
          v-show="prevHabit"
          @click="removeHabit"
          class="ml-2 p-2 border-red-300 border-2 text-red-300 rounded-full cursor-pointer transition-all shadow-lg"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-trash-2 h-6 w-6"
          >
            <polyline points="3 6 5 6 21 6"></polyline>
            <path
              d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"
            ></path>
            <line x1="10" y1="11" x2="10" y2="17"></line>
            <line x1="14" y1="11" x2="14" y2="17"></line>
          </svg>
        </button>
        <button
          v-show="prevHabit"
          @click="cancelEdit"
          class="ml-2 p-2 border-yellow-300 border-2 text-yellow-300 rounded-full cursor-pointer transition-all shadow-lg"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-x h-6 w-6"
          >
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        </button>
        <button
          v-show="prevHabit"
          @click="saveEdit"
          class="ml-2 p-2 border-green-300 border-2 text-green-300 rounded-full cursor-pointer transition-all shadow-lg"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="24"
            height="24"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="feather feather-check h-6 w-6"
          >
            <polyline points="20 6 9 17 4 12"></polyline>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddHabitDialog",
  props: {
    habitStore: Array,
  },
  data() {
    return {
      habits: "",
      prevHabit: "",
    };
  },
  methods: {
    removeHabit() {
      this.$emit("remove", this.prevHabit);
      this.cancelEdit();
    },
    saveEdit() {
      this.$emit("saveEdit", this.habits, this.prevHabit);
      this.cancelEdit();
    },
    cancelEdit() {
      this.prevHabit = "";
      this.habits = "";
    },
    loadHabit(habit) {
      this.prevHabit = habit;
      this.habits = habit;
    },
    saveHabits() {
      this.$emit("save", this.habits);
      this.$emit("toggle");
      this.habits = "";
    },
    closeDialog() {
      this.$emit("toggle");
    },
  },
};
</script>