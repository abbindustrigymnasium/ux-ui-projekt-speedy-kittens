<template>
  <nav class="fixed w-full py-3 bg-gray-700 h-20 blur-xl z-40 font-medium flex justify-center" style="top:0; box-shadow: 0 0 36px 0 rgba(0,10,20,0.8);" >
    <div class="w-5/6 flex items-center justify-between">
      <div class="md:w-1/4">
        <div style="right: 0;">   
            <label for="default-search" class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-gray-300">Search</label>
            <div class="relative">
                <div class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none">
                    <svg aria-hidden="true" class="w-5 h-5 text-yellow-500 dark:text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path></svg>
                </div>
                <input v-model="searchText" type="search" id="default-search" class="block p-4 pl-10 w-full text-sm text-yellow-400 bg-transparent rounded-lg md:border md:border-transparent focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" placeholder="search...">
                <button @click="goToSearch" type="submit" class="hidden md:flex text-white absolute right-2.5 bottom-2.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800" id="navSearchButton">Search</button>
            </div>
        </div>
    </div>

    <div>
        <p class="absolute-center hidden md:block text-yellow-500 text-3xl" style="text-shadow: 0 0 8px rgba(0, 0, 30, 0.8)">F A B U L A</p>
    </div>

      <div class="md:hidden">
        <button @click="drawer">
          <svg
            class="h-8 w-8 fill-current text-black"
            fill="none"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            viewBox="0 0 24 24"
            stroke="orange"
          >
            <path d="M4 6h16M4 12h16M4 18h16"></path>
          </svg>
        </button>
      </div>

      <!-- NavBar -->
      <div class="hidden md:block md:w-1/4 text-gray-200 md:text-xl flex justify-end">
        <ul class="flex space-x-8 font-sans flex justify-end md:list-none">
          <li>
            <nuxt-link
              to="/"
              class=""
              style="text-shadow: 0 0 8px rgba(0, 0, 30, 0.8)"
              >Home</nuxt-link
            >
          </li>
          <li>
            <nuxt-link
              to="/categories"
              class=""
              style="text-shadow: 0 0 8px rgba(0, 0, 30, 0.8)"
              >Categories</nuxt-link
            >
          </li>
          <li>
            <nuxt-link
              to="/staff"
              class=""
              style="text-shadow: 0 0 8px rgba(0, 0, 30, 0.8)"
              >Staff</nuxt-link
            >
          </li>
        </ul>
      </div>

      <transition
        enter-class="opacity-0"
        enter-active-class="ease-out transition-medium"
        enter-to-class="opacity-100"
        leave-class="opacity-100"
        leave-active-class="ease-out transition-medium"
        leave-to-class="opacity-0"
      >
        <div
          @keydown.esc="isOpen = false"
          v-show="isOpen"
          class="z-10 fixed inset-0 transition-opacity"
        >
          <div
            @click="isOpen = false"
            class="absolute inset-0 bg-black opacity-50"
            tabindex="0"
          ></div>
        </div>
      </transition>

      <aside
        class="p-4 transform top-0 left-0 w-64 bg-gray-800 text-white fixed h-full overflow-auto ease-in-out transition-all duration-300 z-30"
        :class="isOpen ? 'translate-x-0' : '-translate-x-full'"
      >
        <div class="close">
          <button
            class="absolute top-0 right-0 mt-4 mr-4"
            @click="isOpen = false"
          >
            <svg
              class="w-6 h-6"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              viewBox="0 0 24 24"
              stroke="gray-800"
            >
              <path d="M6 18L18 6M6 6l12 12"></path>
            </svg>
          </button>
        </div>

        <span
          @click="isOpen = false"
          class="flex w-full items-center p-4 border-b"
        >
          <Tailwind />
        </span>

        <ul class="divide-y font-sans">
          <li>
            <nuxt-link
              to="/"
              class="my-4 inline-block"
              >Home</nuxt-link
            >
          </li>
          <li>
            <nuxt-link
              to="/categories"
              class="my-4 inline-block"
              >Categories</nuxt-link
            >
          </li>
          <li>
            <nuxt-link
              to="/staff"
              class="my-4 inline-block"
              >Meet the Staff</nuxt-link
            >
          </li>
        </ul>
      </aside>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false,
      searchText: ""
    };
  },
  methods: {
    drawer() {
      this.isOpen = !this.isOpen;
    },
    goToSearch() {
      // alert('/search/'+this.searchText);
      this.$router.push('/search/'+this.searchText)
      this.searchText = ""
    }
  },
  watch: {
    isOpen: {
      immediate: true,
      handler(isOpen) {
        if (process.client) {
          if (isOpen) document.body.style.setProperty("overflow", "hidden");
          else document.body.style.removeProperty("overflow");
        }
      },
    },
  },
  mounted() {
    document.addEventListener("keydown", (e) => {
      if (e.keyCode == 27 && this.isOpen) this.isOpen = false;
    });
  },
};
</script>

<style>
.nuxt-link-exact-active {
  border-bottom: 2px solid rgba(255, 136, 80, 0.8);
  padding-bottom: 5px;
}

* {
    font-family:
            'Source Sans Pro',
            -apple-system,
            BlinkMacSystemFont,
            'Segoe UI',
            Roboto,
            'Helvetica Neue',
            Arial,
            sans-serif;
        font-size: 16px;
        word-spacing: 1px;
        -ms-text-size-adjust: 100%;
        -webkit-text-size-adjust: 100%;
        -moz-osx-font-smoothing: grayscale;
        -webkit-font-smoothing: antialiased;
        box-sizing: border-box;
}

#navSearchButton {
    box-shadow: 0 0 12px 0 rgba(0,10,20,0.3);
}

#navSearchButton:hover {
    box-shadow: 0 0 12px 0 rgba(0, 60, 255, 0.3);
}
</style>
