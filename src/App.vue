<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { storeToRefs } from 'pinia';
import { useMessageStore } from './stores/message';
import { useAuthStore } from './stores/auth';
import { useRouter } from 'vue-router';
const store = useMessageStore()
const authStore = useAuthStore()
const router = useRouter()
const token = localStorage.getItem('token')
const user = localStorage.getItem('user')
if (token && user) {
  authStore.reload(token,JSON.parse(user))
}else{
  authStore.logout()
}

const { message } = storeToRefs(store)

function logout(){
  authStore.logout()
  router.push({ name: 'login'})
}

</script>

<template>
  <header class="max-h-screen leading-normal text-center	">
  <h1>Nichakamol Sanghong</h1>   
   <div id="flashMessage" v-if="message">
      <h4 class="font-xl">{{  message  }}</h4>
    </div>
    <nav class="p-8 font-bold text-[#2c3e50]">
      <nav class="flex">
        <ul  v-if="!authStore.currentUserName" class="flex navbar-nav ml-auto">
          <li class="nav-item px-2">
            <router-link to="/register" class="nav-link">
              <font-awesome-icon icon="user-plus" /> Sign Up
            </router-link>
          </li>
          <li class="nav-item px-2">
            <router-link to="/login" class="nav-link">
              <font-awesome-icon icon="sign-in-alt" /> Login
            </router-link>
          </li>
        </ul>
        <ul v-if="authStore.currentUserName" class="flex navbar-nav ml-auto">
        <li class="nav-item px-2">
          <router-link to="/profile" class="nav-link">
            <font-awesome-icon icon="user" />
            {{ authStore.currentUserName }}
          </router-link>
        </li>
        <li class="nav-item px-2">
          <a class="nav-link hover:cursor-pointer" @click="logout">
            <font-awesome-icon icon="sign-out-alt" /> LogOut
          </a>
        </li>
        </ul>
      </nav>
        <RouterLink :to="{name:'EventList'}" class="text-back active:text-green-700 focus:text-green-600">Home</RouterLink> |
        <RouterLink :to="{name:'about'}" class="text-back active:text-green-700 focus:text-green-600">About</RouterLink> |
        <span v-if="authStore.isAdmin">
          <RouterLink :to="{name:'add-event'}" class="text-back active:text-green-700 focus:text-green-600">New Event</RouterLink> |
        </span>
        <RouterLink :to="{name:'add-organizer'}" class="text-back active:text-green-700 focus:text-green-600">New Organizer</RouterLink> |
        <RouterLink :to="{name:'organizer' }" class="text-back active:text-green-700 focus:text-green-600">Organizer</RouterLink> |
        <RouterLink :to="{name:'Student'}" class="text-back active:text-green-700 focus:text-green-600">Student</RouterLink>

      </nav>
  </header>

  <RouterView />
</template>

<style>
#app{
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}


/* nav {
  padding: 30px;
} */

/* nav a.router-link-exact-active {
  color: #42b983;
} */


/* nav a {
  font-weight: bold;
  color: #2c3e50;
} */

/* h4{
  font-size: 20px;
} */

@keyframes yellowfade{
  from{
    background: yellow;
  }
  to{
    background: transparent;

  }
}

#flashMessage{
  animation: yellowfade 3s ease-in-out;
}
</style>