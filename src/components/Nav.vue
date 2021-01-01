<template>
  <div>
    <header class="text-gray-600 body-font">
      <div
        class="container mx-auto flex flex-wrap py-8 px-4 md:px-0 flex-col md:flex-row justify-between items-center"
      >
        <div
          class="flex title-font font-medium items-center text-gray-900 mb-4 md:mb-0"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 511.269 511.269"
            class="w-16 h-16 text-white -ml-2 self-start"
          >
            <path
              d="M140.367 465.067C116.9 438.4 93.434 410.667 78.5 377.6c-14.933-35.2-19.2-75.733-11.733-114.133s24.533-74.667 49.067-105.6c-2.133 26.667 7.467 54.4 25.6 74.667-10.667-51.2 6.4-106.667 40.533-147.2S263.034 18.133 312.1 0c-24.533 25.6-27.733 66.133-18.133 100.267 9.6 34.133 29.867 64 48 94.933 18.133 30.933 35.2 62.933 36.267 98.133 9.6-18.133 20.267-36.267 26.667-56.533 6.4-20.267 9.6-41.6 4.267-61.867 19.2 23.467 29.867 46.933 35.2 76.8 5.333 29.867 4.267 60.8 1.067 90.667-4.267 33.067-12.8 67.2-30.933 94.933-21.333 33.067-55.467 56.533-92.8 69.333C255.567 518.4 190.5 508.8 140.367 465.067z"
              fill="#f3705a"
            />
            <path
              d="M221.434 504.533C308.9 538.667 395.3 435.2 347.3 355.2c0-1.067-1.067-1.067-1.067-2.133 4.267 43.733-6.4 75.733-26.667 93.867 10.667-25.6 3.2-55.467-9.6-81.067-12.8-24.533-30.933-46.933-44.8-70.4-13.867-24.533-24.533-52.267-18.133-80-25.6 19.2-43.733 48-51.2 78.933-7.467 30.933-3.2 65.067 10.667 93.867-16-11.733-27.733-30.933-28.8-51.2-17.067 20.267-27.733 46.933-26.667 73.6.001 41.6 33.067 78.933 70.401 93.866z"
              fill="#ffd15c"
            />
          </svg>
          <div class="flex flex-col items-start">
            <span
              class="ml-1 text-xl md:text-4xl font-mono font-black text-indigo-700"
              >Don't break the chain</span
            >
            <div
              class="flex flex-col md:flex-row items-start ml-1 text-sm font-sans italic text-indigo-500"
            >
              <span class="mr-2"
                >{{ new Date().getFullYear() }} Progression.</span
              >
              <span
                >Project inspired from
                <a
                  class="text-pink-600 self-start"
                  target="_blank"
                  href="https://jamesclear.com/stop-procrastinating-seinfeld-strategy"
                  >this article by James Clear.</a
                ></span
              >
            </div>
            <div class="flex mt-2 ml-1 text-gray-600">
              <a target="_blank" href="https://github.com/manask4/dontbreakthechain" class="bg-gray-200 rounded-full p-2">
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
                  class="feather feather-github h-4 w-4"
                >
                  <path
                    d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
                  ></path>
                </svg>
              </a>
              <a target="_blank" href="https://twitter.com/manask18" class="ml-2 bg-gray-200 rounded-full p-2">
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
                  class="feather feather-twitter h-4 w-4"
                >
                  <path
                    d="M23 3a10.9 10.9 0 0 1-3.14 1.53 4.48 4.48 0 0 0-7.86 3v1A10.66 10.66 0 0 1 3 4s-4 9 5 13a11.64 11.64 0 0 1-7 2c9 5 20 0 20-11.5a4.5 4.5 0 0 0-.08-.83A7.72 7.72 0 0 0 23 3z"
                  ></path>
                </svg>
              </a>
            </div>
          </div>
        </div>
        <button
          @click="toggleDialog"
          class="inline-flex items-center text-white bg-indigo-500 border-0 p-3 focus:outline-none hover:bg-indigo-400 shadow-md hover:shadow-lg transition-all rounded text-base mt-4 md:mt-0"
        >
          Add Habits
        </button>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: "Nav",
  methods: {
    toggleDialog() {
      this.$emit("toggle");
    },
  },
};
</script>