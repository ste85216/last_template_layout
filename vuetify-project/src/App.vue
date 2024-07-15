<template>
  <v-app>
  <v-navigation-drawer v-if="mobile" v-model="drawer">
    <v-list nav>
      <v-list-item v-for="item in navItems" :key="item.to" :prepend-icon="item.icon" :to="item.to" :title="item.text"></v-list-item>
    </v-list>
  </v-navigation-drawer>
  
  
    <v-app-bar>
      <v-container class="d-flex align-center">
        <!-- 左侧 LOGO -->
        <v-img src="./assets/logo-volleycup.png" width="205px" class="logo" />
        <v-spacer></v-spacer>
        <template v-if="mobile">
          <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
        </template>
        <template v-else>
          <v-btn v-for="item in navItems" :key="item.to" :prepend-icon="item.icon" :to="item.to">{{ item.text }}</v-btn>
        </template>
      </v-container>
    </v-app-bar>

    <v-main>
      <swiper></swiper>
  
      <v-container>
        <v-img id="volleyball" src="./assets/volleyball.png" @load="animateVolleyball"></v-img>
        <v-img id="girl" src="./assets/volleyball-girl.png"></v-img>
      </v-container>
      <v-container>
        <v-img id="girl" src="./assets/volleyball-girl.png"></v-img>
      </v-container>
    </v-main>
  </v-app>
</template>f

<script setup>
import { ref, onMounted, nextTick } from 'vue';
import { useDisplay } from 'vuetify';
import swiper from './components/swiper.vue';
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

const { mobile } = useDisplay()

const navItems = [
  { to: '/home', text:"Home", icon:'mdi-home' }, 
  { to: '/aboutus', text:"About Us", icon:'mdi-book' }, 
  { to: '/trainings', text:"Trainings", icon:'mdi-volleyball' }, 
  { to: '/packages', text:"Packages", icon:'mdi-package' }, 
  { to: '/blog', text:"Blog", icon:'mdi-book-open' }, 
  { to: '/contact', text:"Contact", icon:'mdi-phone' }, 
  { to: '/Events', text:"Events", icon:'mdi-history' }, 
]

gsap.registerPlugin(ScrollTrigger);

const animateVolleyball = () => {
  const volleyballEl = document.querySelector('#volleyball');
    gsap.to(volleyballEl, {
      rotation: 360,
      duration: 15,
      repeat: -1,
      repeatDelay: 0,
      ease: 'none',
    })
  }

onMounted(async () => {
  await nextTick(); // 确保DOM已经渲染完成
  animateVolleyball(); // 仅在挂载后调用以检查是否能找到元素
});
</script>

<style lang="scss" scoped>
:deep(.v-toolbar__content) {
  height: 120px !important;
}

::-webkit-scrollbar {
    width: 12px;
}

::-webkit-scrollbar-thumb {
  background: #fff;
}

::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 10px;
}

.swiper {
  margin-top: 41px;
}

.bg-white {
  background-color: white;
}

.logo {
  max-height: 64px;
}

.v-application {
  background: #fff;
}

#volleyball {
  width: 700px;
  height: 700px;
  position: absolute;
  opacity: 0.85;
}

#girl {
  width: 500px;
}
</style>
