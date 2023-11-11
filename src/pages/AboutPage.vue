<template>
  <q-page class="container-home">
    <article>
      <h1>Sobre</h1>
      <p>Projeto desenvolvido para o processo seletivo de desenvolvedor front-end JR/PL da empresa Convicti.</p>
      <p>Todo o código está disponível no <a href="https://github.com/eduardodv/convicti-companies/" target="_blank">Github</a>.</p>
      <br/>
      <h2>Pré-requisitos</h2>
      <ul>
        <li>Utilizar a tecnologia Vue.js ou algum framework derivado, recomendamos o uso do Quasar. (https://quasar.dev/);</li>
        <li>Utilizar como base de dados a API disponibilizada pelo avaliador;</li>
        <li>Utilização de uma tecnologia para exibição de um mapa onde serão agregadas as empresas, recomendamos o Open Layers (https://openlayers.org/).</li>
      </ul>
    </article>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'AboutPage'
});

</script>

<style lang="scss">
  .container-home {
    padding: 3.1rem 1.5rem;
    background-color: $background;

     @media (max-width: $breakpoint-sm-max) {
      padding-top: 2rem;
    }

    article {
      font-size: 1rem;

      h1, h2 {
        font-weight: bold;
        margin: 1rem 0;
        line-height: 1.2;
      }

      h1 {
        font-size: 2.5rem;
      }

      h2 {
        font-size: 1.625rem;
      }

      a {
        color: $secondary;
        text-decoration: none;

        &:hover {
          text-decoration: underline;
        }
      }

      ul {
        padding-left: 1.25rem;

        li {
          margin-bottom: .4375rem;
        }
      }
    }
  }
</style>
