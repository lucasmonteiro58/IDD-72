<template>
  <section class="container">
    <!-- <InitialPage :is-showed="true"></InitialPage> -->
    <!-- <button class="btn btn--primary">
      Conferir Resposta
    </button> -->
    <!-- <StepController></StepController> -->
    <!-- <PopUpObjetivos :is-showed="true"></PopUpObjetivos> -->
    <!-- <CardAnimation
      :card-content="cards"
      :card-index="cardIndex"
    ></CardAnimation>
    <SteperLine class="steper" @next="nextClick" @back="backClick"></SteperLine> -->
  </section>
</template>
<script>
export default {
  mounted() {
    this.$store.commit('changeBackground', 'bg-menu')
  }
}
</script>
<style lang="scss" scoped>
.container {
  @include flex-center;
  flex-direction: column;
}
</style>
