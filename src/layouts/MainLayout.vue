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
        <q-toolbar-title class="q-py-lg">CONVICTI</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      class="bg-primary text-white q-px-xl q-py-lg row"
    >
      <q-list
        class="col flex column justify-between"
      >
        <div>
          <router-link to="/">
            <img
              alt="Quasar logo"
              src="~assets/logo-white.png"
              class="logo"
            >
          </router-link>

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
        </div>

        <q-item
        clickable
        tag="a"
        to="/login"
        class="logout-button col-auto q-mt-xl"
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
      </q-list>
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
  },
  {
    title: 'Sobre',
    icon: 'info',
    route: '/about'
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
    transition: all 0.2s ease;

    @media (hover: hover) {
      &:hover {
        transform: translateX(7px);
      }
    }
  }

  .logout-button {
    border-radius: 6px;
    width: 100%;
  }
</style>
