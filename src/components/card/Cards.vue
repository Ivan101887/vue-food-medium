<template>
  <ul class="cardBox">
    <CardItem v-for="item in parentData" :key="item.ID" :parent-data="item" />
  </ul>
</template>
<script>
import CardItem from './CardItem.vue';

export default {
  name: 'cards',
  props: {
    parentData: Array,
  },
  components: { CardItem },
};
</script>
<style lang="scss" scoped>
  .cardBox {
    display: grid;
    grid: {
      template-columns: repeat(3, 1fr);
      column-gap: 30px;
      row-gap: 30px;
    }
    margin: {
      top: 10px;
    }
    @include pad {
      grid: {
        template-columns: repeat(3, 1fr);
      }
    }
    @include phone-lg {
      margin: {
        top: 0;
      }
    }
  }
</style>
