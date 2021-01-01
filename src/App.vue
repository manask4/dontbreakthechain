<template>
  <div id="app" class="bg-gray-100 min-h-screen">
    <Nav @toggle="toggleDialog" />
    <div :class="isDialogOpen ? 'block' : 'hidden'">
      <add-habit-dialog
        :habitStore="habits"
        @remove="removeHabit"
        @toggle="toggleDialog"
        @save="saveHabits"
        @saveEdit="saveEdit"
      />
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
    saveEdit(latest, previous) {
      let habitStore = localStorage.getItem("habits");
      habitStore = habitStore !== null ? JSON.parse(habitStore) : [];
      var index = habitStore.indexOf(previous);
      if (index !== -1) {
        habitStore[index] = latest;
      }
      localStorage.setItem("habits", JSON.stringify(habitStore));
      this.habits = habitStore;

      let habitStreak = localStorage.getItem("habitStreak");
      habitStreak = habitStreak !== null ? JSON.parse(habitStreak) : {};
      let habitStreakData = habitStreak[previous] ?? [];
      delete habitStreak[previous];
      habitStreak[latest] = habitStreakData;
      localStorage.setItem("habitStreak", JSON.stringify(habitStreak));
      this.habitStreak = habitStreak;
    },
    removeHabit(habit) {
      let habitStore = localStorage.getItem("habits");
      habitStore = habitStore !== null ? JSON.parse(habitStore) : [];
      habitStore = habitStore.filter((item) => item !== habit);
      localStorage.setItem("habits", JSON.stringify(habitStore));
      this.habits = habitStore;

      let habitStreak = localStorage.getItem("habitStreak");
      habitStreak = habitStreak !== null ? JSON.parse(habitStreak) : {};
      delete habitStreak[habit];
      localStorage.setItem("habitStreak", JSON.stringify(habitStreak));
      this.habitStreak = habitStreak;
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
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
