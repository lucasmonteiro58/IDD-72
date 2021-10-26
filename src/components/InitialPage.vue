<template>
  <div v-show="showed" class="initial-page">
    <div class="background-image" :class="background"></div>
    <slot></slot>
    <button
      class="btn btn--primary btn-comecar w375"
      :style="positionButton"
      @click="clickButton"
    >
      {{ textButton }}

      <div class="btn-icon right">
        <BootstrapIcon icon="arrow-right" size="2x" class="trans1" />
      </div>
    </button>
    <div class="info-bottom">
      *Imagens ilustrativas, cores fantasia e mapas sem escala.
    </div>
    <PopUpObjetivos
      v-if="isVisibleObjetivos"
      :is-showed="isVisibleObjetivos"
      @close="closeObjetivos"
      @hide="hideObjetivos"
    ></PopUpObjetivos>
  </div>
</template>

<script>
import { fadeOut } from '../assets/animate'
export default {
  props: {
    textButton: {
      type: String,
      default: 'Comece Agora'
    },
    background: {
      type: String,
      default: 'default-background'
    },
    isShowed: {
      type: Boolean,
      default: true
    },
    bottomButton: {
      type: Number,
      default: 50
    },
    leftButton: {
      type: Number,
      default: 802
    }
  },
  data() {
    return {
      showed: false,
      isVisibleObjetivos: false
    }
  },
  computed: {
    positionButton() {
      return {
        bottom: this.bottomButton + 'px',
        left: this.leftButton + 'px'
      }
    }
  },
  watch: {
    isShowed(val, old) {
      if (!old && val) {
        this.showed = true
        // this.showAnimation()
      } else if (old && !val) {
        this.showed = false
      }
    }
  },
  mounted() {
    if (this.isShowed) this.showed = true
    // this.showAnimation()
  },
  beforeDestroy() {
    fadeOut(this.$el)
  },
  methods: {
    showAnimation() {
      fadeOut(this.$el)
    },
    clickButton() {
      this.openObjetivos()
    },
    openObjetivos() {
      this.isVisibleObjetivos = true
    },
    hideObjetivos() {
      this.isVisibleObjetivos = false
    },
    closeObjetivos() {
      this.$emit('close')
      this.isVisibleObjetivos = false
    }
  }
}
</script>

<style lang="scss" scoped>
.initial-page {
  @include fill-canvas;
  @include flex-center;
  z-index: 1;

  // .slot {
  //   @include fill-canvas;
  // }

  .info-bottom {
    position: absolute;
    bottom: 40px;
    margin-left: -20px;
  }

  .background-image {
    position: absolute;
    top: 0;
    left: 0;
  }

  .default-background {
    width: $canvas-width;
    height: $canvas-height;
    // background-color: blueviolet;
  }

  .btn-comecar {
    position: absolute;
    color: white;
  }
}
</style>
