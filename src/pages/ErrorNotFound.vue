<template>
  <div class="fullscreen bg-primary text-white text-center q-pa-md flex flex-center">
    <div>
      <div class="text-weight-bold" style="font-size: 20vh">
        404
      </div>

      <div class="text-h3" style="opacity:.5">
        Página não encontrada!
      </div>

      <q-btn
        class="q-mt-xl"
        color="secondary"
        text-color="white"
        unelevated
        to="/"
        label="Voltar para a Home"
        no-caps
      />
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ErrorNotFound'
})
</script>
