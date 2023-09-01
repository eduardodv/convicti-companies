<template>
  <q-page class="flex flex-center q-pa-lg">
    <div class="container">
      <img
        alt="Quasar logo"
        src="~assets/logo-white.png"
        class="logo"
      >
      <div>
        <q-form
          @submit="onSubmit"
          @reset="onReset"
        >

          <q-input
            v-model="email"
            label="E-mail"
            stack-label
            lazy-rules
            bg-color="white"
            label-color="white"
            :rules="[ val => val && val.length > 0 || 'Por favor, insira um e-mail!', isValidEmail]"
          />

          <q-input
            v-model="password"
            label="Senha"
            type="password"
            stack-label
            lazy-rules
            bg-color="white"
            label-color="white"
            class="q-pb-sm"
            :rules="[ val => val && val.length > 0 || 'Por favor, insira uma senha!,']"
          />

          <div>
            <q-btn label="Entrar" type="submit" color="secondary" class="full-width" size="md"/>
          </div>
        </q-form>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import { useQuasar } from 'quasar'
import { ref } from 'vue'
import { useRouter } from 'vue-router';

export default defineComponent({
  name: 'LoginPage',

  setup () {
    const $q = useQuasar()
    const router = useRouter()

    const email = ref(null)
    const password = ref(null)


    return {
      email,
      password,

      onSubmit () {
        // email.value = null
        // password.value = null

        $q.notify({
          color: 'green-9',
          textColor: 'white',
          icon: 'login',
          message: 'Logado com sucesso!'
        })

        // test redirect
        router.push({ path: '/' })
      },
    }
  },
  methods: {
    isValidEmail (val) {
      const emailPattern = /^(?=[a-zA-Z0-9@._%+-]{6,254}$)[a-zA-Z0-9._%+-]{1,64}@(?:[a-zA-Z0-9-]{1,63}\.){1,8}[a-zA-Z]{2,63}$/;
      return emailPattern.test(val) || 'Por favor, insira um e-mail válido!';
    }
  }
});


</script>

<style lang="scss">
  body {
    color: $white;
    background-color: $primary;
  }

  .container {
    width: 100%;
    max-width: 400px;
  }

  .logo {
    width: 300px;
    display: block;
    margin: 0 auto 5rem;
    max-width: 100%;
  }

  form {
    .q-field {
      &__control {
        border-radius: 6px;
        &:after {
          display: none;
        }
      }

      &__control, &__append {
        height: 36px;
      }

      &__label {
        top: -1rem;
        transform: none;
        font-size: 1.2rem;
      }

      &__native {
        padding: 0.3rem 1rem !important;
      }

      &__bottom {
        position: relative;
        overflow: hidden;
        padding: 0;
      }

      &__bottom--animated {
        transform: translateY(3px);
      }
    }
  }
</style>
