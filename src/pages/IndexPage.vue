<template>
  <q-page class="container-home">
    <header class="row">
      <div class="col-12 col-sm-7 col-md-5">
        <q-input
          v-model="search"
          type="search"
          placeholder="Pesquisar"
          class="input-search"
          outlined
        >
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>
      </div>
      <div class="col-12 col-sm-5 col-md-7 text-right">
        <q-btn icon-right="add" label="Adicionar Empresa" class="button-add" @click="showModalCompanies = !showModalCompanies" />
      </div>
    </header>

    <MapCompanies ref="map" />

    <ModalCompanies
      @refreshCompanies="refreshCompanies"
      v-model="showModalCompanies"
    />

  </q-page>
</template>

<script>
import { api } from 'src/boot/axios'
import { defineComponent, onMounted, ref } from 'vue'

import ModalCompanies from 'components/ModalCompanies.vue'
import MapCompanies from 'components/MapCompanies.vue'

export default defineComponent({
  name: 'IndexPage',

  components: {
    ModalCompanies,
    MapCompanies,
  },

  setup () {
    const search = ref(null)
    const showModalCompanies = ref(false)
    const map = ref(null)

    const refreshCompanies = () => {
      map.value.loadCompanies()
    }

    return {
      search,
      showModalCompanies,
      map,
      refreshCompanies
    }
  }
});

</script>

<style lang="scss">
  .container-home {
    padding: 1.5rem;
    background-color: $background;

    header {
      @media (max-width: $breakpoint-xs-max) {
        > div {
          &:last-child {
            order: -1;
          }
        }
      }
    }

    .input-search {
      background-color: $white;
      border-radius: 8px;

      ::placeholder { color: #bbb }

      i {
        color: #bbb
      }

      .q-field {
        &__control {
          font-size: 1rem;

          &:before {
            border: 0;
          }

          &:after {
            border-radius: 8px;
          }
        }
      }

      &.q-field--highlighted {
        .q-field__control {
          &:after {
            border-color: #ddd;
          }
        }
      }
    }

    .button-add {
      height: 100%;
      font-size: 1rem;
      border-radius: 6px;
      line-height: 1;
      text-transform: capitalize;
      background: $background-light;

      &:before {
        display: none;
      }

      &:hover {
        color: $white;
        background: $primary;
      }

      @media (max-width: $breakpoint-xs-max) {
        width: 100%;
        height: 56px;
        margin-bottom: 1rem;
      }
    }
  }
</style>
