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
          <p>The transition towards a low carbon future requires large changes in the production, conversion and use of energy.
            Such large changes impose risks to actors and investors in the sectors that are involved in these activities.
            For example, costs may increase, cost structures will change, revenues could increase or decrease and the need
            for investments in new equipment may go up as well. In these modules, we guide you through the main risks related
            to the transition to a low-carbon future to the fossil fuel sector, the power sector and the end-use sectors.
          </p>
        </IntersectionObserver>
        <IntersectionObserver :step="1"  align="left">
          <div class="sticky">
            <h3 class ="module-title">1 Fossil Fuels Risk</h3>
              <p>
                Mitigation of climate change is a highly contested issue since it affects the use of fossil fuels, which
                contributes 85% of global primary energy supply. Therefore, it is seen as the basis for economic production
                and income and, thus, socioeconomic prosperity. The  key role of fossil fuels in the world economy makes fossil
                resources valuable assets at the moment, but their value may change in the future if climate mitigation efforts
                are serious and the energy sector successfully transitions to a low-carbon future.
                <a class="moduleLink" href   ="https://climatescenarios.org/fossil-fuels/" target="_blank">↗ Module 1: Fossil Fuels Risk</a>
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
            Large parts of our energy system and economy depend on fossil fuels and will be affected by efforts to reduce
            CO2 emissions. The rapid development of renewable energy technology and the pricing of carbon to reduce CO2
            emissions under mitigation scenarios, will drive a transition in the power sector towards low-carbon energy
            technologies. The significant ramp-up of these technologies will require large investments. Hence, climate
            policies will redirect investments and will lead to revaluation of assets. <br>
            <a href="https://climatescenarios.org/power-sector/" target="_blank" class="moduleLink">↗ Module 2: Power Sector Risk</a>
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
            Many final energy uses in the industry, transport and buildings sectors depend on fossil fuels and will be
            affected once fossil fuels are phased out and renewables ramped up. Options to improve energy efficiency
            will become more competitive at higher energy prices but require increased investments.
            <br>
            <a href="https://dev.climatescenarios.org/end-use/" target="_blank" class="moduleLink">↗ Module 3: Enduse Risk</a>
          </p>
        </div>
        <div class="spacer">
            &nbsp;
        </div>
        </IntersectionObserver>
        <IntersectionObserver :step="4"  align="left" class="lastheight">
          <p>
            To facilitate a smooth transition towards broad and deep emission reductions, climate policies need to
            strengthen gradually, and this revaluation and redirection will happen in a differentiated way.
            <br> However, there is no guarantee that the transition will be smooth, and strong climate policies might be
            imposed on short notice.
            Explore the three modules on Transition Risks to find out more.
          </p>
        </IntersectionObserver>
      </div>
      </LayoutScrollytelling>
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
      .moduleLink {
        fill: getColor(neon, 40);
        font-weight: normal;
        text-decoration: none;
        background: none;
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
