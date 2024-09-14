<template>
  <q-layout>
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title>
          LIGHTBEARER
        </q-toolbar-title>

        <div class="list">
          
          <ul>
            <li>Home</li>
            <li>Services</li>
            <li>Gallery</li>
            <li>Contact</li>
          </ul>
          </div>
        
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
    style="background-color: aliceblue;">
      <q-list>

    <div>
    <q-img src="https://cdn.quasar.dev/img/material.png" style="height: 150px;"></q-img>
  </div>
    <div class="user-info" style="margin-top: 0px; text-align: center;">
      <q-avatar class="q-mb-sm">
        <img src="~assets/6648.jpg" style="margin-top: -40px; position: absolute; width: 100px; height: 100px;">
      </q-avatar>
      <div class="text-weight-bold">JPR</div>
      <div>@jprigdao@gmail.com</div>
    </div>


        <div style="flex-grow: 1;"></div>

        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'

defineOptions({
  name: 'MainLayout'
})

const linksList = [
  {
    title: 'Home',
    // caption: 'quasar.dev',
    icon: 'home',
    link: 'https://quasar.dev'
  },
  {
    title: 'Services',
    // caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework'
  },
  {
    title: 'Gallery',
    // caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev'
  },
  {
    title: 'Forum',
    // caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev'
  },
  {
    title: 'Contact',
    // caption: '@quasarframework',
    icon: 'phone',
    link: 'https://twitter.quasar.dev'
  }
]

const leftDrawerOpen = ref(false)

function toggleLeftDrawer () {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>
