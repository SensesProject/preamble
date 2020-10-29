<template>
  <div id="app">
    <SensesMenu :id="'power-sector'"/>
    <div class="content" :class="mobile ? 'isMobile' : 'isDesktop'" ref="container">
      <h1 class="header">Preamble <br>Transition Risks </h1>
      <LayoutScrollytelling>
        <template v-slot:vis="{ width, height, step }">
          <div class="vis-inner" :style="{width: `${width}px`, height: `${height}px`}">
            <RiskPathwayIllu :width="width" :height="height" :step="step"/>
          </div>
        </template>
        <div slot="text" class="observer">
        <IntersectionObserver :step="0"  align="left" class="firstheight">
          <p>Lorem ipsum Mitigation of climate change is a highly contested issue since it affects the use of fossil fuels,
            which contributes 85% of global primary energy supply. Therefore, it is seen as the basis for economic
            production and income and, thus, socioeconomic prosperity.
            Their key role in the world economy makes fossil fuel deposits valuable assets at the moment.
          </p>
        </IntersectionObserver>
        <IntersectionObserver :step="1"  align="left">
          <div class="sticky">
            <h3 class ="module-title">1 Fossil Fuels Risk</h3>
              <p>
                Lorem ipsum In the scenarios, this transition is driven by a carbon tax that increases the relative costs per MWh
                of fossil fuels compared to renewables and other low-carbon technologies Mitigation of climate change
                is a highly contested issue since it affects the use of fossil fuels,
                which contributes 85% of global primary energy supply. Therefore, it is seen as the basis for economic
                production and income and, thus, socioeconomic prosperity.
                <!-- <br>
                <br>
                <a href   ="https://dev.climatescenarios.org/preamble/#" target="_blank" class="to-module">↗ Module 1</a> -->
              </p>
          </div>
          <div class="spacer">
              &nbsp;
          </div>
        </IntersectionObserver>
        <IntersectionObserver :step="2"  align="left">
          <div class="sticky">
          <h3 class="module-title">2  Power Sector Risk</h3>
          <p>
            Lorem ipsum in the scenarios, this transition is driven by a carbon tax that increases the relative costs per MWh
            of fossil fuels compared to renewables and other low-carbon technologies Mitigation of climate change
            is a highly contested issue since it affects the use of fossil fuels,
            which contributes 85% of global primary energy supply. Therefore, it is seen as the basis for economic
            production and income and, thus, socioeconomic prosperity.
            <!-- <br>
            <br>
            <a href="https://dev.climatescenarios.org/preamble/#" target="_blank" class="to-module">↗ Module 2</a> -->
          </p>
          </div>
          <div class="spacer">
              &nbsp;
          </div>
        </IntersectionObserver>
        <IntersectionObserver :step="3"  align="left">
        <div class="sticky">
          <h3 class="module-title">3  Enduse Risk</h3>
          <p>
            Lorem ipsum in the scenarios, this transition is driven by a carbon tax that increases the relative costs per MWh
            of fossil fuels compared to renewables and other low-carbon technologies Mitigation of climate change
            is a highly contested issue since it affects the use of fossil fuels,
            which contributes 85% of global primary energy supply. Therefore, it is seen as the basis for economic
            production and income and, thus, socioeconomic prosperity.
            <!-- <br>
            <br>
            <a href="https://dev.climatescenarios.org/preamble/#" target="_blank" class="to-module">↗ Module 3</a> -->
          </p>
        </div>
        <div class="spacer">
            &nbsp;
        </div>
        </IntersectionObserver>
        <IntersectionObserver :step="4"  align="left" class="lastheight">
          <p>
            Lorem ipsum as a result, total revenues within the power sector (based on the MWh’s produced times the electricity
            price) shifts from fossil utilities to low-carbon based utilities. Issue since it affects the use of
            fossil fuels, which contributes 85% of global primary energy supply. Issue since it affects the use of
            fossil fuels, which contributes 85% of global primary energy supply. Issue since it affects the use of
            fossil fuels, which contributes 85% of global primary energy supply. Issue since it affects the use of
            fossil fuels, which contributes 85% of global primary energy supply.
          </p>
        </IntersectionObserver>
      </div>
      </LayoutScrollytelling>
      <!-- <SensesMeta :id="'power-sector'"/> -->
    </div>
  </div>
</template>

<script>
import SensesMenu from 'library/src/components/SensesMenu.vue'
import LayoutScrollytelling from 'library/src/components/LayoutScrollytelling.vue'
import IntersectionObserver from 'library/src/components/IntersectionObserver.vue'
import RiskPathwayIllu from './components/RiskPathwayIllu.vue'

export default {
  name: 'App',
  components: {
    LayoutScrollytelling,
    IntersectionObserver,
    RiskPathwayIllu,
    SensesMenu
  },
  data () {
    return {
      width: 0,
      height: 0
    }
  },
  computed: {
    mobile () {
      let isMobile = false
      if (this.width < 750) { isMobile = true }
      return isMobile
    }
  },
  methods: {
    calcSizes () {
      const { container: el } = this.$refs
      const totalWidth = el.clientWidth
      const totalHeight = el.clientHeight || el.parentNode.clientHeight
      this.width = Math.max(totalWidth, 400)
      this.height = Math.max(totalHeight, 400)
    }
  },
  mounted () {
    this.calcSizes()
    window.addEventListener('resize', this.calcSizes, false)
  },
  updated () {
    this.calcSizes()
  },
  beforeDestroy () {
    window.removeEventListener('resize', this.calcSizes, false)
  }
}
</script>

<style lang="scss">
@import "library/src/style/base.scss";
@import "library/src/style/variables.scss";

#app {
  margin: 0 auto;
  .senses-menu .bar {
    background: none;
    backdrop-filter: none;
    //background-size: 30% auto;
  }
  .content {
    max-width: 100%;
    margin: 0 auto;

    .header {
      transition: background $transition;
      background: transparentize($color-white, 0.02);
        @supports (
          (-webkit-backdrop-filter: saturate(180%) blur(20px)) or
            (backdrop-filter: saturate(180%) blur(20px))
        ) {
          background: transparentize($color-white, 0.15);
          -webkit-backdrop-filter: saturate(180%) blur(10px);
          backdrop-filter: saturate(180%) blur(10px);
        }
      z-index: 10;
      margin-left: 2vh;
      width: 30%;
      padding: 15vh 0 3vh 2vh;
      position: fixed;
      top: 0;
    }
    .module-title {
      // color: getColor(violet, 60);
    }
    .to-module {
      text-decoration: none;
      text-align: center;
      padding: .5rem 1rem;
      border: 1px solid #d8d8e4;
      border-radius: 2px;
      pointer-events: all;
      background: none;
      color: black;
      margin-top: 10px;
    }
    .intersection-observer {
      width: 30%;
      padding: 4vh 0 2vh 2vh;

      &.firstheight{
        padding-top: 26vh;
        padding-bottom: 0vh;
      }
      &.lastheight{
        padding-bottom: 25vh;
      }
    }
    .sticky {
      position: sticky;
      align-self: start;
      top: 30vh;
    }
    .spacer {
    width: 30%;
    height: 200px;
    }

    &.isMobile {
      .header {
        width: 100%;
      }
      .intersection-observer {
        width: 100%;
        &.firstheight{
          padding-top: 60vh
        }
      }
    }
  }
}
</style>
