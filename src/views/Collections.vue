<template>
    <transition-group tag="div" class="collections" @beforeEnter="beforeEnter" @leave="leave" @enter="enter" appear>
    <product-b v-for="(item, index) in items" :key="`el+${index}`" :data-index="index"/>
  </transition-group>
</template>

<script>
import {ref} from 'vue';
import {gsap} from 'gsap';
import ProductB from '@/components/ProductB';

export default {
  name: 'Collections',
  setup() {
    const items = ref([
      {}, {}, {}, {}, {}, {}, {}, {}
    ])

    const beforeEnter = (el) => {
      debugger;
      el.style.opacity = '0';
      el.style.transform = 'translateY(-30px)';
    };

    const enter = (el, done) => {
      gsap.to(el, {
        opacity: 1,
        y: 0,
        duration: 1,
        onComplete: done,
        delay: el.dataset.index * 0.3
      })
    };

    return { items, beforeEnter, enter };
  },
  components: {
    ProductB
  }
}
</script>

<style lang="scss">
.collections {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  flex: 1;
}
</style>
