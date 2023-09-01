<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="lt-md none">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      class="bg-primary text-white q-px-xl q-py-lg row column"
    >
      <q-list
        class="col"
      >
        <img
          alt="Quasar logo"
          src="~assets/logo-white.png"
          class="logo"
        >

        <q-item-label
          header
          class="q-px-none text-white"
        >
          MENU
        </q-item-label>

        <MenuLink
          v-for="link in menuLinks"
          :key="link.title"
          v-bind="link"
        />

      </q-list>
      <q-item
        clickable
        tag="a"
        to="/login"
        class="logout-button col-auto q-mr-lg"
      >
        <q-item-section
          avatar
          class="q-pr-sm"
          :style="'min-width: 30px'"
        >
          <q-icon name="power_settings_new" />
        </q-item-section>

        <q-item-section>
          <q-item-label>Sair</q-item-label>
        </q-item-section>
      </q-item>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import MenuLink from 'components/MenuLink.vue'

const linksList = [
  {
    title: 'Empresas',
    icon: 'domain',
    route: '/'
  }
]

export default defineComponent({
  name: 'MainLayout',

  components: {
    MenuLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {
      menuLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>

<style lang="scss">
  .logo {
    width: 100%;
    margin: 2.2rem 0 4rem;
  }

  .logout-button {
    border-radius: 6px;
    width: 100%;
    margin: 0;
  }
</style>
