<template>
  <q-item
    clickable
    tag="a"
    :to="route"
    class="custom-link text-labels"
    active-class="custom-link-active"
  >
    <q-item-section
      v-if="icon"
      avatar
      class="q-pr-sm"
      :style="'min-width: 35px'"
    >
      <q-icon :name="icon" />
    </q-item-section>

    <q-item-section>
      <q-item-label>{{ title }}</q-item-label>
    </q-item-section>
  </q-item>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'MenuLink',
  props: {
    title: {
      type: String,
      required: true
    },

    route: {
      type: String,
      default: '#'
    },

    icon: {
      type: String,
      default: ''
    }
  }
})
</script>

<style lang="scss">
  .custom-link {

    border-radius: 6px;
    color: $white;
    font-size: 1rem;
    margin-bottom: 0.5rem;

    .q-item__label {
      line-height: 1 !important;
    }
  }

  .custom-link-active {
    color: $labels;
    background-color: $white;
  }
</style>
