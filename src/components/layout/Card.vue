<template>
  <div class="content-card">
    <div class="backdrop"></div>
    <div class="card card--rounded">
      <button class="btn btn--icon" @click="close">
        <BootstrapIcon icon="x-lg" size="2x" class="trans9" />
      </button>
      <div class="card-image">
        <ZoomImage v-if="imgBig" class="zoom-image" :image="imgBig"></ZoomImage>
        <div :class="image" class="imageee">
          <div class="creditos" v-html="creditos"></div>
        </div>

        <div class="font" v-html="font"></div>
      </div>
      <div class="card-content">
        <div class="title">{{ title }}</div>
        <div class="text" v-html="text"></div>
      </div>
    </div>
  </div>
</template>

<script>
import { scaleOut, scaleIn } from '../../assets/animate'
export default {
  props: {
    title: {
      type: String,
      default: 'Usinas Hidréletricas'
    },
    image: {
      type: String,
      default: ''
    },
    text: {
      type: String,
      default:
        'Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam possimus, maxime architecto quam ipsum magnam distinctio non ipsam sunt eos. Eaque debitis, ut vitae dolores eius fugiat soluta dolorum officia.'
    },
    creditos: {
      type: String,
      default: ''
    },
    font: {
      type: String,
      default: ''
    },
    isShowed: {
      type: Boolean,
      required: false,
      default: true
    },
    imgBig: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      showed: false
    }
  },
  watch: {
    isShowed(val, old) {
      if (!old && val) {
        this.showed = true
        this.showAnimation()
      } else if (old && !val) {
        this.showed = false
      }
    }
  },
  mounted() {
    if (this.isShowed) this.showed = true
    this.showAnimation()
  },
  beforeDestroy() {
    scaleOut(this.$el)
  },
  methods: {
    showAnimation() {
      scaleIn(this.$el.lastChild)
    },
    close() {
      this.$emit('close')
    }
  }
}
</script>

<style lang="scss">
.content-card {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: center;

  .backdrop {
    position: absolute;
    background-color: #00000060;
    width: 100%;
    height: 100%;
  }
}
.card--rounded {
  z-index: 2;
  display: flex;
  justify-content: space-between;
  padding: $gap * 2;
  position: relative;
  .btn--icon {
    z-index: 2;
    position: absolute;
    top: 42px;
    right: 42px;
  }

  .card-image {
    @include flex-center;
    flex-direction: column;
    width: 533px;
    margin-top: 30px;

    .imageee {
      position: relative;
    }

    .creditos {
      position: absolute;
      top: 40px;
      left: -25px;
      writing-mode: vertical-lr;
      transform: rotate(180deg);
      text-transform: uppercase;
      color: #6e6e6e;
    }

    .zoom-image {
      position: absolute;
      top: 100px;
      left: 50px;
    }

    .font {
      margin-top: 20px;
      font-size: 1.05rem;
      text-align: center;
      padding: 0 40px;
    }
  }

  .card-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    margin-left: 20px;
    width: 637px;

    .title {
      @include font-neosans-black;
      font-size: 2.25rem;
      font-weight: 900;
      margin-bottom: $gap;
    }

    .text {
      font-size: 1.5rem;
      padding-right: $gap * 3.7;
    }
  }
}
</style>
