
<template>
  <a-card :bordered="false">
    <template v-for="api in apiList" :key="api.id">
      <api-card />
    </template>
  </a-card>
</template>


<script>
import ApiCard from './components/ApiCard/index.vue'

export default {
  data() {
    return {
      apiList: [
        {
          "id": "aaa"
        },
        {
          "id": "bbb"
        },
        {
          "id": "bbb"
        },
        {
          "id": "bbb"
        }
      ]
    };
  },
  methods: {},
  mounted() {
    console.log("xxxxxxxxxxxxx");
  },
  components: { ApiCard }
}
</script>


<style>
@import './assets/base.css';
</style>
