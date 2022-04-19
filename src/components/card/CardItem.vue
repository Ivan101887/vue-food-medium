<template>
  <li class="card">
    <div class="card__wrap">
      <figure class="card__imgWrap">
        <img
          :src="parentData.PicURL"
          :alt="parentData.Name"
          class="card__img"
          loading="lazy"
        />
      </figure>
      <p class="card__tag">{{ parentData.City }}</p>
      <div class="card__content">
        <em class="card__town">{{ parentData.Town }}</em>
        <h2 class="card__name">{{ parentData.Name }}</h2>
        <p class="card__desc">{{ parentData.HostWords }}</p>
      </div>
    </div>
  </li>
</template>
<script>
export default {
  name: 'card-parentData',
  props: {
    parentData: Object,
  },
};
</script>
<style lang="scss" scoped>
  .card {
    // width: (100% / 3);
    // @include pad {
    // width: (100% / 2);
    // }
    // @include phone-md {
    // padding: 10px 10px 0 10px;
    // }
    // @include phone-lg {
    // width: 100%;
    // padding: {
    // bottom: 0;
    // }
    // }
    // padding: 15px;
    box-sizing: border-box;
    &__wrap {
      position: relative;
      overflow: hidden;
      box-sizing: border-box;
      &:hover {
        .card {
          &__imgWrap {
            transform: scale(1.05);
          }
          &__content {
            bottom: 12px;
          }
        }
      }
    }
    &__imgWrap {
      height: 200px;
      &::after {
        content: "";
        position: absolute;
        top: 0;
        display: block;
        width: 100%;
        height: 100%;
        background: {
          image: linear-gradient(
            to bottom,
            rgba(0, 0, 0, 0) 0%,
            rgba(0, 0, 0, 0.3) 70%,
            rgba(0, 0, 0, 0.8) 100%
          );
        }
      }
      transition: all 0.5s ease-in;
    }
    &__img {
      display: block;
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
    &__tag {
      position: absolute;
      top: 0;
      font: {
        size: 12px;
      }
      color: #fff;
      background: {
        color: #e49400;
      }
      padding: 5px;
    }
    &__content {
      position: absolute;
      bottom: -54px;
      color: #fff;
      max-width: 100%;

      padding: {
        left: 12px;
      }
      transition: all 0.5s ease-in;
    }
    &__town {
      opacity: 0.6;
      display: block;
      margin: {
        bottom: 5px;
      }
      font: {
        size: 15px;
      }
    }
    &__name {
      font: {
        weight: 400;
      }
      &::after {
        content: "";
        display: block;
        width: 48px;
        margin: {
          top: 10px;
          bottom: 10px;
        }
        border: {
          top: 2px solid #fff;
          bottom: 2px solid #fff;
        }
      }
    }
    &__desc {
      font: {
        size: 14px;
      }
      height: 38px;
      overflow: hidden;
      line-height: 1.35em;
    }
  }
</style>
