<template>
  <q-page class="flex flex-center">
    <!-- <img
      alt="Quasar logo"
      src="~assets/quasar-logo-vertical.svg"
      style="width: 200px; height: 200px"
    > -->
    <h1>Home</h1>
    {{ data }}
  </q-page>
</template>

<script>
import { useQuasar } from 'quasar'
import { api } from 'src/boot/axios'
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'IndexPage',
});


</script>
