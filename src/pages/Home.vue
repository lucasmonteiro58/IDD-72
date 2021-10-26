<template>
  <section class="container">
    <div class="infos-top-layout">
      <div class="title-top">Alguns conflitos territoriais da atualidade</div>
      <div class="subtitle-top">
        Clique nos destaques no mapa para saber mais.
      </div>
    </div>
    <div class="content-map">
      <div v-if="!showInitialPage">
        <!-- <sequential-entrance delay="80"> -->
        <div
          v-for="content in contents"
          :key="content.id"
          class="icon-toclick"
          :class="{ visited: content.visited }"
          :style="{
            top: content.top,
            left: content.left,
            animationDelay: `${content.delay}s`
          }"
          @click="openCard(content)"
        >
          <div
            class="icon-cc"
            :class="content.icon"
            :style="{ animationDelay: `${content.delay + 0.2}s` }"
          ></div>
          <div
            class="legenda"
            :style="{ top: content.legendaTop, left: content.legendaLeft }"
          >
            {{ content.title }}
          </div>
        </div>
        <!-- </sequential-entrance> -->
      </div>
    </div>
    <Card
      v-if="isVisibleCard"
      class="card-map"
      :is-showed="isVisibleCard"
      :image="currentContent.image"
      :title="currentContent.title"
      :text="currentContent.text"
      :font="currentContent.font"
      :creditos="currentContent.creditos"
      :img-big="currentContent.imgBig"
      @close="closeCard"
    ></Card>
    <div class="info-bottom">
      *Imagens ilustrativas, cores fantasia e mapas sem escala.
    </div>
  </section>
</template>
<script>
import { contents } from '../consts/home.js'
export default {
  data() {
    return {
      contents,
      currentContent: contents[0],
      isVisibleCard: false
    }
  },
  computed: {
    showInitialPage() {
      return this.$store.state.initialPageState
    }
  },
  watch: {
    showInitialPage(newValue, oldValue) {
      this.contents.forEach((el) => {
        el.visited = false
      })
    }
  },
  methods: {
    openCard(content) {
      this.changeActualContent(content)
      content.visited = true
      this.isVisibleCard = true
    },
    closeCard() {
      this.isVisibleCard = false
    },
    changeActualContent(content) {
      this.currentContent = content
    }
  }
}
</script>
<style lang="scss" scoped>
.container {
  @include flex-center;
  flex-direction: column;

  .info-bottom {
    position: absolute;
    bottom: 40px;
    margin-left: -20px;
  }

  .icon-toclick {
    position: absolute;
    cursor: pointer;
    transition: 0.3s;
    opacity: 0;
    animation-name: bounceIn;
    animation-duration: 450ms;
    animation-timing-function: linear;
    animation-fill-mode: forwards;

    &:hover {
      filter: drop-shadow(1px 1px 5px white);
    }

    &.visited {
      .icon-cc {
        opacity: 0.5 !important;
      }
    }

    .legenda {
      position: absolute;
      width: 100px;
      @include font-neosans-black;
    }

    .icon-cc {
      // animation: float 6s ease-in-out infinite;
      position: absolute;
    }
  }

  .card-map {
    z-index: 1;
  }
}
</style>
