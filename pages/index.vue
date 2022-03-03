<template>
  <layout-wrapper>
    <layout-header />
    <layout-visual
      title="小人旅人ブログ"
      message="旅の情報を伝えるブログです。楽しんでください。"
      :imgPath="
        require('~/assets/img/7be2179f-1220-4ef1-9888-e7e427a4d9f1-0.jpg')
      "
      color="text-light"
    />
    <base-heading>おすすめの旅行先</base-heading>
    <div class="conatainer-fluid">
      <div class="card-deck row flex-row flex-nowrap overflow-auto">
        <layout-vertical-menu
          v-for="(trip, index) in trips"
          :className="'col-7 col-md-5'"
          :key="index"
          :title="trip.title"
          :description="trip.description"
          :imgPath="trip.image1.url"
          :isTrancate="true"
          imgWidth="100%"
          imgHeight="300px"
        />
      </div>
    </div>
    <base-button
      ><a href="/trip" class="btn btn-primary text-center"
        >旅行先一覧</a
      ></base-button
    >
    <base-heading>お知らせ</base-heading>
    <layout-information
      v-for="(information, index) in informations"
      :key="index"
      :time="information.date"
      :title="information.information"
    ></layout-information>
    <base-button
      ><a href="/information" class="btn btn-primary text-center"
        >お知らせ一覧</a
      ></base-button
    >
    <layout-footer />
  </layout-wrapper>
</template>

<script>
import LayoutFooter from "../components/LayoutFooter.vue";
import LayoutVerticalMenu from "../components/LayoutVerticalMenu.vue";
import LayoutWrapper from "../components/LayoutWrapper.vue";
import axios from "axios";

function getData (config) {
  return Promise.all([
    axios
      .get(config.apiURL + "trip", {
        headers: { "X-MICROCMS-API-KEY": config.apiKey },
      }),
      axios
      .get(config.apiURL + "information", {
        headers: { "X-MICROCMS-API-KEY": config.apiKey },
      }),
  ]).then(([trips, informations]) => {
    const data = {}
    data.trips = trips.data.contents
    data.informations = informations.data.contents
    return Promise.resolve(data)
  })
}

export default {
  components: { LayoutWrapper, LayoutFooter, LayoutVerticalMenu },
  name: "IndexPage",

  async asyncData({ $config }) {
    const data = await getData($config)
    return {
      trips: data.trips,
      informations: data.informations,
    }
  },  
};
</script>