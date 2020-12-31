<template>
  <div>
    <div class="habits flex flex-wrap px-10 mb-2">
      <span
        class="m-2 px-2 py-1 text-sm bg-yellow-200 rounded-md cursor-pointer transition-all shadow-md"
        v-for="(habit, index) in habits"
        :key="index"
        @click="updateActiveHabit(habit)"
        :class="
          activeHabit === habit ? 'bg-yellow-400' : 'text-gray-600'
        "
        >{{ habit }}
      </span>
    </div>
    <div class="flex flex-wrap justify-start px-10">
      <span
        class="m-2 border border-gray-100 p-5 h-16 w-16 rounded-full shadow-sm hover:shadow-md cursor-pointer transition-all"
        :class="habitDone(n) ? 'bg-green-300' : ''"
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
    defaultHabit: function() {
      return this.habits[0] || '';
    }
  },
  methods: {
    updateActiveHabit(habit) {
      this.activeHabit = habit;
    },
    toggleHabitStreak(day) {
      this.$emit('toggleStreak', day, this.habitDone(day), this.activeHabit);
    },
    habitDone(day) {
      const habitData = this.habitStreak[this.activeHabit] ?? [];
      return habitData.includes(day);
    },
  },
  mounted() {
    this.activeHabit = this.defaultHabit;
  },
  watch: {
    habits: function() {
      this.activeHabit = this.activeHabit || this.habits[0];
    }
  },
};
</script>

<style scoped>
.active {
  background-color: green;
}
</style>