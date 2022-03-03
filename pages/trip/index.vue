<template>
  <layout-wrapper>
    <layout-header />
    <layout-visual
      title="旅行先"
      message="おすすめの旅行先を紹介します。"
      color="text-light"
      :height="50"
      :imgPath="
        require('~/assets/img/acc13280-34db-4e85-a57d-8d05eedeb959-0.jpg')
      "
    />
    <base-heading>おすすめの旅行先</base-heading>
    <div class="container">
      <div class="mb-10">
        <layout-side-menu
          :key="index"
          v-for="(item, index) in items"
          :title="item.title"
          :description="item.description"
          ><carousel height="300px" width="100%" :images="items[index].images"
        /></layout-side-menu>
      </div>
    </div>
    <base-button
      ><a href="/" class="btn btn-primary">トップページ</a></base-button
    >
    <layout-footer />
  </layout-wrapper>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      items,
      imageName: String
    };
  },
  async asyncData({ $config }) {
    await axios
      .get($config.apiURL + "trip", {
        headers: { "X-MICROCMS-API-KEY": $config.apiKey },
      })
      .then((response) => {
        self.items = response.data.contents;
        for (let i = 0; i < response.data.contents.length; i++) {
          self.items[i]["images"] = [];
          for (let j = 0; j < 5; j++) {
            self.imageName = "image" + (j + 1);
            if (response.data.contents[i].hasOwnProperty(imageName)) {
              self.items[i]["images"].push(response.data.contents[i][imageName]);
            }            
          }
        }
      }).catch(error => {
        console.log(error);
      });
  },
};
</script>
