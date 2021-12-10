<template>
  <button type="button" @click="fillClick">-fill-</button>
  <button type="button" @click="clearClick">-clear-</button>
  <div style="display: flex;">
    <div v-for="s in steps" class="" :key="s.id">
      <div>{{ s.id }}</div>
        <div v-for="(a) in getList(s.id)" :key="a.id" style="border: 1px solid gray; margin: 2px;">
          <div>element with dynamic value - {{ a.id }}</div>
          <div :key="a.id">element with key</div>
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

    const getList = function (a:string) {
      let _a: {id: string, name:string}[] = [];
      for (let i = 0; i < 3000; i++) {
        _a.push({
          id: 'item_id_' + a + i,
          name: 'item_name_' + a + i
        })
      }
      return _a;
    };

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
      getList,
      clearClick,
      fillClick
    }
  },
});
</script>
