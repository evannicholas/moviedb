<template>
  <q-layout view="lHh Lpr lFf">
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

        <q-toolbar-title> MovieDB </q-toolbar-title>

        <div>
          <q-btn color="primary" icon="check" @click="toggleDarkMode" />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered class="bg-grey-8">
      <q-list>
        <q-item-label header class="text-grey-1">
          Essential Links
        </q-item-label>

        <EssentialLink
          v-for="link in essentialLinks"
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

<script>
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    title: "Home",
    icon: "school",
    link: "/",
  },
  {
    title: "Search",
    icon: "school",
    link: "search",
  },
  {
    title: "Movie",
    icon: "school",
    link: "movie",
  },
];

import { defineComponent, ref, onMounted } from "vue";
import { useQuasar } from "quasar";

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },

  setup() {
    const leftDrawerOpen = ref(false);
    const $q = useQuasar();
    const toggleDarkMode = () => {
      $q.dark.toggle();
    };

    onMounted(() => {
      $q.dark.set(true)
    })

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleDarkMode,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
