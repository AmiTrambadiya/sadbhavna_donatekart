<template>
  <div class="pt-2 pl-2 md:pl-4 lg:pl-24 pr-2 md:pr-4 lg:pr-24">
    <div class="rounded-xl bg-[#40b751]">
      <nav class="px-6 md:px-6 lg:px-6 sm:py-2 md:py-8 lg:py-8 mx-auto md:flex md:justify-between md:items-center">
        <div class="flex  justify-between">
          <div class="flex items-center flex-shrink-0">
            <img src="../../src/assets/Inter/img/logo.png"
              class="mb-2 lg:mb-0 sm:mt-2 lg:mt-0 mr-32 w-28 lg:w-48 h-16 lg:h-44 ml-0 lg:ml-6" />
          </div>
          <!-- Mobile menu button -->
          <div @click="showMenu = !showMenu" class="flex md:hidden">
            <button type="button" class="text-white hover:text-white focus:outline-none focus:text-white">
              <svg viewBox="0 0 24 24" class="w-6 h-6 fill-current">
                <path fill-rule="evenodd"
                  d="M4 5h16a1 1 0 0 1 0 2H4a1 1 0 1 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2zm0 6h16a1 1 0 0 1 0 2H4a1 1 0 0 1 0-2z ">
                </path>
              </svg>
            </button>
          </div>
        </div>
        <!-- Mobile Menu open: "block", Menu closed: "hidden" -->
        <ul :class="showMenu ? 'flex' : 'hidden'"
          class="flex-col mt-8 space-y-4 md:flex md:space-y-0 md:flex-row md:items-center md:space-x-4 lg:space-x-6 md:mt-0">
          <li>
            <a href="/home" class="font-bold text-white hover:text-black">Home</a>
          </li>
          <li>
            <a href="#" class="font-bold text-white hover:text-black">About</a>
          </li>
          <li>
            <a href="/sadbhavna/request-campaign" class="font-bold text-white hover:text-black">Request a Campaign</a>
          </li>
          <li>
            <a href="/sadbhavna/contact-us" class="font-bold text-white hover:text-black">Contact</a>
          </li>
          <li>
            <span class="group relative inline-block">
              <a href="#" class="font-bold text-white hover:text-black">Blog</a>
              <ul class="absolute hidden pt-1  group-hover:block">
                <li class=""><a class="whitespace-pre block bg-white py-2 px-4" href="/sadbhavna/blog">Blog</a></li>
                <li class=""><a class="whitespace-pre block bg-white py-2 px-4" href="#">Single - Blog</a></li>
              </ul>
            </span>
          </li>
          <li>
            <span class="group lg:inline-block">
              <a href="#" class="font-bold text-white hover:text-black">Page</a>
              <ul class="absolute hidden group-hover:block">
                <li class=""><a class="whitespace-pre block bg-white py-2 px-4" href="#">Elements</a></li>
                <li class=""><a class="whitespace-pre block bg-white py-2 px-4" href="#">Cause</a></li>
              </ul>
            </span>
          </li>
          <li v-if="this.user.isLoggedIn()" @click="profile()"
            class="font-bold text-white hover:text-black cursor-pointer">
            profile
          </li>
          <li>
            <button v-if="this.user.isLoggedIn()" @click="logout()"
              class="bg-white text-black font-medium text-base mt-2 mb-2 lg:mb-0 mr-4 pt-2 pb-2 pl-8 pr-8 transition duration-300 rounded hover:bg-[#40b751] hover:text-white hover:outline hover:outline-1 hover:outline-offset-1">Logout</button>
            <button v-else @click="this.$router.push(`/sadbhavna/login`)"
              class="bg-white text-black font-medium text-base mt-2 mb-2 lg:mb-0 mr-4 pt-2 pb-2 pl-8 pr-8 transition duration-300 rounded hover:bg-[#40b751] hover:text-white hover:outline hover:outline-1 hover:outline-offset-1">Login</button>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { inject } from "vue";
export default {
  name: "Navbar",
  setup() {
    const user = inject("user")
    return {
      user
    }
  },
  data() {
    return {
      showMenu: false
    }
  },
  methods: {
    logout() {
      console.log("click logout")
      axios.get('/api/method/logout').then((res) => {
        this.$router.go()
      }).catch(function (error) {
        console.log("not okey")
      })
    },

    profile() {
      const cookie = Object.fromEntries(
        document.cookie
          .split("; ")
          .map((part) => part.split("="))
          .map((d) => [d[0], decodeURIComponent(d[1])])
      )
      this.$router.push(`/sadbhavna/profile/${cookie.user_id}`)
    }

  },

  mounted() {
    if (!this.user.isLoggedIn()) {
      // this.$router.push({
      // 	name: "DeskLogin",
      // 	query: { route: this.$route.path },
      // })
      return
    }
    // else{
    //   this.$router.push(`/sadbhavna/login`) 
    // }
    // if (!this.user.has_desk_access) {
    // 	this.$router.push({ path: "/home" })
    // 	return
    // }
  }
}
</script>



