<template>
  <div class="container mx-auto w-4/5 md:w-1/2 mb-4">
    <div class="bg-indigo-500 p-6 flex flex-col rounded-md shadow-lg">
      <p class="self-start text-md font-bold text-white mb-2">
        Add Habits to track
      </p>
      <input
        v-model="habits"
        required
        placeholder="Reading, Writing, Exercise, Journaling..."
        class="border h-10 px-4 rounded-md"
        type="text"
      />
      <p class="text-xs text-gray-200 mt-1">
        Enter single or multiple habits separated by a comma. For eg:
        Reading,Writing,Exercise
      </p>
      <div class="flex justify-end">
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
    </div>
  </div>
</template>

<script>
export default {
  name: "AddHabitDialog",
  data() {
    return {
      habits: "",
    };
  },
  methods: {
    saveHabits() {
      this.$emit("save", this.habits);
      this.$emit("toggle");
    },
    closeDialog() {
      this.$emit("toggle");
    },
  },
};
</script>