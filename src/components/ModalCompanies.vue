<template>
  <q-dialog v-model="modalCompanies" position="right" full-height class="modal-companies">
    <q-card class="flex column no-wrap" style="width: 800px; max-width: 100vw;">
      <q-card-section class="q-pa-none">
        <div class="title-modal text-h5">
          <strong>Cadastrar Empresa</strong>
        </div>
      </q-card-section>
      <q-card-section class="q-pa-none modal-content">
        <q-form
          @submit="handleSubmit"
          @reset="onReset"
          greedy
          ref="formRef"
        >
          <div class="row q-col-gutter-x-lg">
            <div class="col-12 col-sm-6">
              <div>
                <span>Nome</span>
                <q-input
                  outlined
                  v-model="form.name"
                  lazy-rules
                  :rules="[
                    val => val && val.length > 0 || 'Por favor, digite o nome da empresa.'
                  ]"
                />
              </div>
              <div>
                <span>CNPJ</span>
                <q-input
                  outlined
                  v-model="form.cnpj"
                  lazy-rules
                  mask="##.###.###/####-##"
                  :rules="[
                    val => val && val.length > 0 || 'Por favor, digite o CNPJ da empresa.',
                    val => val && val.length > 17 || 'CNPJ inválido!',
                  ]"
                />
              </div>
              <div>
                <span>E-mail</span>
                <q-input
                  outlined
                  v-model="form.email"
                  lazy-rules
                  :rules="[
                    val => val && val.length > 0 || 'Por favor, digite o E-mail da empresa.',
                  ]"
                />
              </div>
              <div>
                <span>Whatsapp</span>
                <q-input
                  outlined
                  v-model="form.whatsapp"
                  lazy-rules
                  type="tel"
                  mask="(##) #####-####"
                  :rules="[
                    val => val && val.length > 0 || 'Por favor, digite o Whatsapp da empresa.',
                    val => val && val.length > 13 || 'Whatsapp inválido!',
                  ]"
                />
              </div>
              <div>
                <span>Representante</span>
                <q-input
                  outlined
                  v-model="form.representative"
                />
              </div>
              <div class="row q-col-gutter-x-md">
                <div class="col-12 col-md-6">
                  <span>Latitude</span>
                  <q-input
                    outlined
                    v-model="form.lat"
                    lazy-rules
                    :rules="[
                      val => val && val.length > 0 || 'Por favor, digite a Latitude.',
                    ]"
                  />
                </div>
                <div class="col-12 col-md-6">
                  <span>Longitude</span>
                  <q-input
                    outlined
                    v-model="form.long"
                    lazy-rules
                    :rules="[
                      val => val && val.length > 0 || 'Por favor, digite a Longitude.',
                    ]"
                  />
                </div>
              </div>
              <div class="row q-col-gutter-x-md">
                <div class="col-12 col-md-6">
                  <span>Estado</span>
                  <q-select
                    outlined
                    v-model="form.state"
                    :options="statesList"
                    :rules="[
                      val => val && val.length > 0 || 'Por favor, selecione um Estado.',
                    ]"
                  />
                </div>
                <div class="col-12 col-md-6">
                  <span>Cidade</span>
                  <q-select
                    outlined
                    v-model="form.city"
                    :options="citiesList"
                    :rules="[
                      val => val && val.length > 0 || 'Por favor, selecione uma Cidadade.',
                    ]"
                  />
                </div>
              </div>
            </div>
            <div class="col-12 col-sm-6">
              <div>
                <span>Observações</span>
                <q-input
                  outlined
                  v-model="form.observations"
                />
              </div>
              <div>
                <span>Categoria</span>
                <q-select
                    outlined
                    v-model="form.categories"
                    :options="categoriesList"
                    :rules="[
                      val => val && val.length > 0 || 'Por favor, selecione uma Categoria.',
                    ]"
                  />
              </div>
            </div>
          </div>
        </q-form>
      </q-card-section>

      <q-card-actions class="q-pa-none" align="center">
        <q-btn flat label="Cancelar" class="btn btn-cancel" v-close-popup />
        <q-btn label="Cadastrar Empresa" @click="submitForm" class="btn btn-confirm" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<script>
import { computed, defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'ModalCompanies',

  props: {
    modelValue: {
      type: Boolean
    },
  },

  setup (props, {emit}) {
    const modalCompanies = computed({
      get() {
        return props.modelValue
      },
      set(newValue) {
        emit('update:modelValue', !props.modelValue)
      }
    })

    const formRef = ref(null)

    const form = ref({
      cnpj: '',
      email: '',
      whatsapp: '',
      representative: '',
      lat: '',
      long: '',
      state: '',
      city: '',
      observations: '',
      categories: '',
    })

    const statesList = ['DF', 'PR', 'SC']
    const citiesList = ['Brasília', 'Guarapuava', 'Itapema']
    const categoriesList = ['Cat1', 'Cat2', 'Cat3']

    const submitForm = () => {
      formRef.value.submit()
    }

    const handleSubmit = () => {
      console.log(form.value);
    }

    return {
      modalCompanies,
      formRef,
      form,
      statesList,
      citiesList,
      categoriesList,
      submitForm,
      handleSubmit,
    }
  }
})
</script>

<style lang="scss">
  .modal-companies {
    .q-dialog {
      &__inner {
        padding: 0;
      }
    }

    .q-card {
      padding: 2rem 3rem;
      background: $background;
      border-radius: 0;

      @media (max-width: $breakpoint-xs-max) {
        padding-left: 1.5rem;
        padding-right: 1.5rem;
      }
    }

    .title-modal {
      margin-top: 1rem;
      color: $labels;

      @media (max-width: $breakpoint-xs-max) {
        margin-top: 1rem;
      }
    }

    .modal-content {
      flex: 1;
      color: $labels;
      padding: 1rem 0 2.5rem;

      .q-field {
        padding-bottom: 20px;
        margin-top: 3px;

        &__control,
        &__native {
          height: 40px;
          min-height: 40px;
        }

        &__control {
          border-radius: 6px;
          background-color: $white;

          > div {
            height: inherit;
          }

          input {
            color: $labels;
          }

          &:before {
            border-color: #ddd;
          }
        }

        &__bottom {
          padding: 4px 0 0 0;
        }

        &__messages {
          white-space: nowrap;
        }
      }
    }

    .btn {
      width: 180px;
      height: 46px;
      text-transform: capitalize;
      border-radius: 6px;
      color: $labels;
      background-color: #eee;

      &.btn-confirm {
        color: $white;
        background-color: $labels;
      }

      @media (max-width: $breakpoint-xs-max) {
        margin: 5px;

        &+.btn {
          margin-left: 5px;
        }
      }
    }
  }
</style>
