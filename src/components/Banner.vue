<template>
  <section class="banner" id="banner" :style="style" data-speed="3">
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <section class="banner__content">
            <slot></slot>
          </section>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: ["image", "height", "positionY"],
  data: () => ({
    speed: 3
  }),
  computed: {
    style() {
      return {
        height: `calc(${this.height} - 61.5px)`,
        background:
          "linear-gradient(to bottom, rgba(0, 0, 0, 1) 0%, rgba(41, 55, 150, 0.5) 100%), url(" +
          this.image +
          ")",
        backgroundSize: "cover",
        backgroundPosition: `center ${this.positionY}`
      };
    }
  },
  mounted() {
    let isMobile = window.matchMedia("only screen and (max-width: 768px)")
      .matches;

    if (!isMobile) {
      var banner = document.getElementById("banner");
      window.addEventListener("scroll", () => {
        var yPos = window.pageYOffset / this.speed;
        var coords = `center calc(${this.positionY} + ${yPos}px)`;
        banner.style.backgroundPosition = coords;
      });
    }
  }
};
</script>

<style lang="scss" scoped>
.banner {
  display: flex;
  align-items: center;
  .banner__content {
    color: #fff;
  }
}
</style>