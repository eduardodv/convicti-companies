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

    <section class="map-container"></section>

    <ModalCompanies v-model="showModalCompanies" :states="states" />

  </q-page>
</template>

<script>
import { api } from 'src/boot/axios'
import { defineComponent, onMounted, ref } from 'vue'

import ModalCompanies from 'components/ModalCompanies.vue'

export default defineComponent({
  name: 'IndexPage',

  components: {
    ModalCompanies
  },

  setup () {
    const search = ref(null)
    const showModalCompanies = ref(false)
    const states = ref([])

    const loadStates = async () => {
      const response = await api.get('/api/state-cities/states')
      states.value = response.data.map((state) => {
        return {
          label: state.letter,
          value: state.id
        }
      })
    }

    onMounted(() => {
      loadStates()
    })

    return {
      search,
      states,
      showModalCompanies
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

    .map-container {
      width: 100%;
      height: calc(100vh - 120px);
      border-radius: 18px;
      margin-top: 16px;
      background-color: $dark;
    }
  }
</style>
