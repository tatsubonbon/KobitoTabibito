<template>
  <div class="carousel-wrapper" :style="'width:' + currentWidth">
    <div :style="'width:' + currentWidth">
      <img
        :src="target.url"
        alt=""
        style="object-fit: cover"
        :style="{ width: currentWidth, height: currentHeight}"
      />
    </div>
    <!--START: カルーセルのテンプレート -->
    <transition tag="div" :name="imageTransitionName">
      <div class="carousel-item" :key="target.id">
        <img
          :src="target.url"
          alt=""
          style="object-fit: cover"
          :style="{ width: currentWidth, height: currentHeight}"
        />
      </div>
    </transition>
    <!--END: カルーセルのテンプレート -->
    <!--START: ページャーのテンプレート -->
    <ol class="carousel-pager" v-if="images.length > 1">
      <li v-for="(image, index) in images" :key="image.id">
        <button
          tabindex="0"
          :class="{ isCurrent: index === selectedIndex }"
          @click="onClickPager(index)"
        ></button>
      </li>
    </ol>
    <!--END: ページャーのテンプレート -->
    <!--START: PREV / NEXTボタンのテンプレート -->
    <button
      v-if="images.length > 1"
      class="carousel-control-prev"
      type="button"
      data-bs-target="#carouselExampleControls"
      data-bs-slide="prev"
      @click="onClickPrev"
    >
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden"></span>
    </button>
    <button
      v-if="images.length > 1"
      class="carousel-control-next"
      type="button"
      data-bs-target="#carouselExampleControls"
      data-bs-slide="next"
      @click="onClickNext"
    >
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden"></span>
    </button>
    <!--END: PREV / NEXTボタンのテンプレート -->
  </div>  
</template>

<script>
export default {
  name: "Carousel",
  props: {
    width: {
      type: String
    },
    height: {
      type: String
    },
    images: {
      default: () => [
        {
          id: 1,
          url: "https://placehold.jp/300x300.png",
        },
        {
          id: 2,
          url: "https://placehold.jp/300x300.png",
        },
        {
          id: 3,
          url: "https://placehold.jp/300x300.png",
        },
      ],
    },
  },
  data: function () {
    return {
      // 現在表示しているカルーセルの幅、高さ
      currentWidth: this.width,
      currentHeight: this.height,
      // 現在表示しているカルーセル画像のインデックス
      selectedIndex: 0,
      // トランジション名 prev OR next
      imageTransitionName: "prev",
    };
  },
  computed: {
    // 現在表示しているカルーセル画像オブジェクト
    target: function () {
      const self = this;
      return this.images[self.selectedIndex];
    },
    // 最後のカルーセル画像のインデックス
    lastIndex: function () {
      return this.images.length - 1;
    },
  },
  methods: {
    // ドットをクリックしたときのメソッド
    onClickPager: function (index) {
      // 選択したドットのインデックスが選択していた画像のインデックスより
      // 前か後ろかでトランジション名を変更する
      this.imageTransitionName = this.selectedIndex < index ? "next" : "prev";
      this.selectedIndex = index;
      // 選択中のインデックスに引数で受け取ったインデックスをセット
      this.setTargetHeight(index); //img要素の親に高さをセット
    },
    // PREVボタンををクリックしたときのメソッド
    onClickPrev: function () {
      this.imageTransitionName = "prev";
      // 最初の画像で「PREV」を押下した場合、最後の画像を表示する
      this.selectedIndex =
        this.selectedIndex <= 0 ? this.lastIndex : this.selectedIndex - 1;
      this.setTargetHeight(this.selectedIndex);
    },
    // NEXTボタンををクリックしたときのメソッド
    onClickNext: function () {
      this.imageTransitionName = "next";
      // 最後の画像で「NEXT」を押下した場合、最初の画像を表示する
      this.selectedIndex =
        this.selectedIndex >= this.lastIndex ? 0 : this.selectedIndex + 1;
      this.setTargetHeight(this.selectedIndex);
    },
    // 受け取ったインデックス番号の画像の高さを取得してimg要素の親に高さをセットするメソッド
    setTargetHeight: function (index) {
      const img = new Image();
      const self = this;
      img.src = this.images[index].src;
    },
  },
  mounted: function () {
    this.setTargetHeight(this.selectedIndex);
  },
};
</script>

<style scoped>
/* カルーセルに関連する要素のスタイリング
  ================================*/
.carousel-wrapper {
  width: 100%;
  overflow: hidden;
  margin: auto;
  position: relative;
}

.carousel-item {
  width: 100%;
}
.carousel-item > img {
  vertical-align: top;
}

.carousel-navigation {
  padding: 0;
  margin: 20px 0;
  list-style: none;
}
.carousel-navigation > li {
  display: inline-block;
}

.carousel-pager {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  text-align: center;
  padding: 0;
  margin: 20px 0;
  list-style: none;
}
.carousel-pager > li {
  display: inline-block;
  margin: 0 5px;
}
.carousel-pager > li > button {
  appearance: none;
  border: none;
  background-color: #999;
  width: 16px;
  height: 16px;
  border-radius: 8px;
}

.carousel-pager > li > button.isCurrent {
  background-color: #f00;
}
</style>
