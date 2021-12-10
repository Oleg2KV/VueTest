<template>
  <button type="button" @click="fillClick">-=fill-</button>
  <button type="button" @click="clearClick">-=clear-</button>
  <div style="display: flex;">
    <div v-for="(s, index) in steps" class="" :key="s.id">
      <div>{{ s.id }}</div>
      <div>
          <div>element with dynamic value - {{ index }}</div>
          <div :key="s.id+'__'+index">element with key</div>
          <div>element with static text</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, onMounted, ref} from 'vue';

export default defineComponent({
  name: 'Home',
  components: {
  },

  setup() {

    const steps = ref<{ id: string}[]>([]);
    const c = ref(1);

    const fill = function () {
      let _steps: { id: string }[] | null = [];
      for (let i = c.value!; i < (c.value! + 10); i++) {
        _steps.push({id: 's_' + i})
      }
      steps.value = _steps;
      _steps = null;
    }

    onMounted(()=>{
      // fill();
    });

    fill();

    const clear = function () {
      steps.value = [];
    }

    const clearClick = () => {
      clear();
    }
    const fillClick = () => {
      fill();
    }

    return {
      steps,
      clearClick,
      fillClick
    }
  },
});
</script>
