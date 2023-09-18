<template>
 
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'mainPage',
  data() {
    return {
  
    };
  },
  methods: {
    emitEvent() {
      this.$emit('myEvent', 'Данные события');
    },
  },
  
});
</script>

<style>


</style>