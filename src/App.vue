<template>
  <div id="app" class="bg-gray-100 min-h-screen">
    <Nav @toggle="toggleDialog" />
    <div :class="isDialogOpen ? 'block' : 'hidden'">
      <add-habit-dialog @toggle="toggleDialog" @save="saveHabits" />
    </div>
    <div class="container mx-auto py-5 bg-white rounded-md shadow-md">
      <calendar
        @toggleStreak="toggleHabitStreak"
        :habits="habits"
        :habitStreak="habitStreak"
      />
    </div>
    <!-- <front-page msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
import Calendar from "./components/Calendar.vue";
import Nav from "./components/Nav.vue";
import AddHabitDialog from "./components/AddHabitDialog.vue";

export default {
  name: "App",
  components: {
    Calendar,
    AddHabitDialog,
    Nav,
  },
  data() {
    return {
      isDialogOpen: false,
      habits: [],
      habitStreak: {},
    };
  },
  methods: {
    toggleDialog() {
      this.isDialogOpen = !this.isDialogOpen;
    },
    saveHabits(userHabits) {
      let habitStore = localStorage.getItem("habits");
      habitStore = habitStore !== null ? JSON.parse(habitStore) : [];

      userHabits = userHabits
        .split(",")
        .map((item) => {
          item = item.trim();
          return item.charAt(0).toUpperCase() + item.slice(1);
        })
        .filter((item) => item.length > 0 && !habitStore.includes(item));

      habitStore.push(...userHabits);
      this.habits = [...habitStore];
      localStorage.setItem("habits", JSON.stringify(habitStore));
    },
    toggleHabitStreak(day, state, activeHabit) {
      let habitStreak = localStorage.getItem("habitStreak");
      habitStreak = habitStreak !== null ? JSON.parse(habitStreak) : {};
      let habitData = habitStreak[activeHabit] ?? [];
      if (state) {
        habitData = habitData.filter((item) => item !== day);
      } else {
        habitData.push(day);
      }

      habitStreak[activeHabit] = habitData;
      this.habitStreak = habitStreak;
      localStorage.setItem("habitStreak", JSON.stringify(habitStreak));
    },
  },
  mounted() {
    const habitStore = localStorage.getItem("habits");
    this.habits = habitStore !== null ? JSON.parse(habitStore) : [];

    const habitStreak = localStorage.getItem("habitStreak");
    this.habitStreak = habitStreak !== null ? JSON.parse(habitStreak) : {};
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
