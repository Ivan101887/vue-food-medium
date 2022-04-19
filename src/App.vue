<template>
  <div id="app">
    <TheLoader v-if="isLoading" />
    <TheHeader :parent-title="title" />
    <main class="main container mx-auto">
      <div class="form">
        <FilterSelect
          parent-name="行政區"
          parent-id="City"
          :parent-data="cityArr"
          @update="updateCurrentCity"
        />
        <FilterSelect
          parent-name="行政區"
          parent-id="Town"
          :parent-data="townArr"
          @update="updateCurrentTown"
        />
      </div>
      <Cards :parent-data="filterData" />
    </main>
    <TheFooter :parent-title="source.info" :parent-src="source.src" />
  </div>
</template>

<script>
import TheHeader from '@/components/layout/TheHeader.vue';
import TheFooter from '@/components/layout/TheFooter.vue';
import TheLoader from '@/components/TheLoader.vue';
import Cards from '@/components/card/Cards.vue';
import FilterSelect from '@/components/FilterSelect.vue';

export default {
  name: 'App',
  components: {
    TheHeader,
    TheFooter,
    TheLoader,
    Cards,
    FilterSelect,
  },
  data() {
    return {
      title: '農場地方美食小吃料理',
      source: {
        info: '政府資料開放平台',
        src: 'https://data.gov.tw/dataset/6037',
      },
      current: {
        city: '',
        town: '',
      },
      data: [],
      isLoading: true,
    };
  },
  async created() {
    await this.getData();
    this.isLoading = !this.isLoading;
  },
  computed: {
    cityArr() {
      return Array.from(new Set(this.data.map((item) => item.City)));
    },
    townArr() {
      return Array.from(
        new Set(
          this.data.filter((item) => item.City === this.current.city).map((item) => item.Town),
        ),
      );
    },
    filterData() {
      if (this.current.city) {
        if (!this.current.town) {
          return this.data.filter((item) => item.City === this.current.city);
        }
        return this.data
          .filter((item) => item.City === this.current.city)
          .filter((item) => item.Town === this.current.townl);
      }
      return this.data;
    },
  },
  methods: {
    async getData() {
      try {
        const api = 'https://data.coa.gov.tw/Service/OpenData/ODwsv/ODwsvTravelFood.aspx';
        const res = await this.$http.get(api);
        this.data = res.data;
      } catch (e) {
        console.log('資料連結失敗:\n', e);
      }
    },
    updateCurrentCity(val) {
      this.current.city = val;
    },
    updateCurrentTown(val) {
      this.current.town = val;
    },
  },
};
</script>

<style lang="scss" scoped>
  .form {
    text: {
      align: center;
    }
    background: {
      color: #fff;
    }
    border: {
      radius: 5px;
    }
    padding: {
      top: 20px;
      bottom: 20px;
    }
    @include phone-md {
      margin: {
        left: 10px;
        right: 10px;
      }
    }
    @include phone-lg {
      padding: {
        top: 0;
        bottom: 0;
      }
      background: {
        color: transparent;
      }
    }
  }
</style>
