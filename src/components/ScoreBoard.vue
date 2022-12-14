<template>
  <div>
    <section class="score">
      Player <span>{{ this.winCount }}</span> x
      <span>{{ this.loseCount }}</span> Computer
    </section>
  </div>
</template>

<script>
export default {
  props: ["winCount", "loseCount"],
};
</script>

<style lang="scss">
section.score {
  border-bottom: 1px solid #000000;
  padding: 24px;
  font-size: 18px;
  font-weight: 600;

  span {
    padding: 8px;
    font-weight: bold;
    border: 1px solid #000000;
  }
}
</style>