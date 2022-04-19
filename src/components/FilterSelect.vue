<template>
  <select
    class="form__sel"
    :id="parentId"
    @change="$emit('update', $event.target.value)"
  >
    <option class="form__option" value="" :selected="!parentData.length">
      請選擇{{ parentName }}
    </option>
    <option
      class="form__option"
      v-for="item in parentData"
      :key="item"
      :value="item"
    >
      {{ item }}
    </option>
  </select>
</template>
<script>
export default {
  name: 'filter-select',
  props: {
    parentId: String,
    parentName: String,
    parentData: Array,
  },
};
</script>
<style lang="scss" scoped>
  .form {
    &__sel {
      width: 25%;
      border: {
        radius: 5px;
        width: 0;
      }
      font: {
        size: 15px;
      }
      appearance: none;
      background: {
        image: url("@/assets/image/down-arrow.png");
        repeat: no-repeat;
        size: 6px 12px;
        position: 98% 50%;
        color: #ddd;
      }
      padding: 10px 0 10px 10px;
      margin: {
        left: 15px;
        right: 15px;
      }
      @include phone-lg {
        width: 100%;
        margin: {
          left: 0;
          right: 0;
        }
        & + & {
          margin: {
            top: 15px;
          }
        }
      }
    }
    &__option {
      background: {
        color: #fff;
      }
    }
  }
</style>
