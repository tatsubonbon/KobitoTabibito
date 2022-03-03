<template>
  <layout-wrapper>
    <layout-header />
    <layout-visual
      title="お知らせ"
      color="text-light"
      :height=20
      :imgPath="require('~/assets/img/bd5db043-88b6-40d1-befd-7660997d476c-0.jpg')"
    />
    <base-heading>お知らせ一覧</base-heading>
    <layout-information
      v-for="(information, index) in informations"
      :key="index"
      :time="information.date"
      :title="information.information"
    ></layout-information>
    <layout-footer />
  </layout-wrapper>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      informations,
    };
  },
  async asyncData({ $config }) {
    await axios
      .get($config.apiURL + "information", {
        headers: { "X-MICROCMS-API-KEY": $config.apiKey },
      })
      .then((response) => {
        self.informations = response.data.contents;
      }).catch(error => {
        console.log(error);
      });
  },
};
</script>