<template>
  <div>
    <div class="flex flex-wrap px-10 mb-2">
      <span
        class="m-2 px-3 py-2 text-sm bg-yellow-100 rounded-full cursor-pointer transition-all shadow-xl hover:shadow-lg"
        v-for="(habit, index) in habits"
        :key="index"
        @click="updateActiveHabit(habit)"
        :class="
          activeHabit === habit ? 'bg-yellow-500 text-white' : 'text-yellow-600'
        "
        >{{ habit }}
      </span>
    </div>
    <div class="text-center flex flex-wrap justify-start px-10">
      <span
        class="m-2 p-5 h-16 w-16 rounded-full border transition-all focus:outline-none"
        :class="{
          'bg-green-300': habitDone(n),
          'bg-gray-100 text-gray-400': !isEnabled(n),
          'cursor-pointer text-gray-700 shadow-md hover:shadow-lg': isEnabled(n),
        }"
        v-for="n in 365"
        :key="n"
        @click="toggleHabitStreak(n)"
        >{{ n }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calendar",
  props: {
    habits: Array,
    habitStreak: Object,
  },
  data() {
    return {
      activeHabit: "",
    };
  },
  computed: {
    defaultHabit: function () {
      return this.habits[0] || "";
    },
  },
  methods: {
    dateDiff() {
      const dateObj = new Date();
      const month = ("0" + (dateObj.getMonth() + 1)).slice(-2);
      const day = ("0" + dateObj.getDate()).slice(-2);
      const year = dateObj.getFullYear();
      const currentDate = year + "-" + month + "-" + day;

      const startDate = "2021-01-01";
      const diffInMs = new Date(currentDate) - new Date(startDate);
      const diffInDays = diffInMs / (1000 * 60 * 60 * 24) + 1;
      return diffInDays;
    },
    updateActiveHabit(habit) {
      this.activeHabit = habit;
    },
    toggleHabitStreak(day) {
      if (this.isEnabled(day)) {
        this.$emit("toggleStreak", day, this.habitDone(day), this.activeHabit);
      }
    },
    habitDone(day) {
      const habitData = this.habitStreak[this.activeHabit] ?? [];
      return habitData.includes(day);
    },
    isEnabled(day) {
      const currentDay = this.dateDiff();
      return this.habits.length > 0 && currentDay >= day;
    },
  },
  mounted() {
    this.activeHabit = this.defaultHabit;
  },
  watch: {
    habits: function () {
      if (!this.habits.includes(this.activeHabit) || !this.activeHabit) {
        this.activeHabit = this.habits[0];
      }
    },
  },
};
</script>

<style scoped>
.active {
  background-color: green;
}
</style>