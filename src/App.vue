<template>
  <div id="app" class="transitional app" v-bind:class="current_colour">
      <div
        class="about-drop"
        v-bind:class="{ active: isActive }"
      >
        <div class="wrapper">
          <h2>{{msg}}</h2>
          <h3>For the times in our lives when we need words of wisdom from a higher power that embraces big hair and rhinestones.</h3>
          <p>Made with <i class="fa fa-heart"></i> by <a href="http://www.allisontarr.com">Allison Tarr</a></p>
        </div>
      </div> <!--/.about-drop-->

      <header>
        <div class="wrapper">
          <button
            class="about-button"
            v-bind:class="{ active: isActive }"
            v-on:click="isActive = !isActive"
          >
            <p class="screen-reader-text">Menu</p>
            <span class="mobile-menu-bar line-1"></span>
            <span class="mobile-menu-bar line-2"></span>
            <span class="mobile-menu-bar line-3"></span>
          </button>

          <div class="card">
            <h1>{{msg}}</h1>
          </div>

          <div class="twitter">
            <a href="http://twitter.com/share?text=%22It%27s+hard+to+be+a+diamond+in+a+rhinestone+world.%22&url=http://whatwoulddollydo.com&via=allisonplus&hashtags=wwdd"><span class="screen-reader-text">Share this site via Twitter</span><i class="fa fa-twitter" aria-hidden="true"></i></a>
          </div> <!--/.twitter-->
        </div> <!--/.wrapper-->
      </header>

    <section class="content">
      <tabs>
          <tab name="Lorem">
            <Lorem/>
          </tab>

          <tab name="Quotes" :selected="true">
            <Quotes
              v-bind:getRandomNumber="getRandomNumber"
              v-bind:getRandomColour="getRandomColour"
            >
            </Quotes>
          </tab>
      </tabs>
    </section> <!--/.content-->
  </div>
</template>

<script>
import Lorem from './components/Lorem.vue';
import Quotes from './components/Quotes.vue';
import Tabs from './components/Tabs.vue';
import Tab from './components/Tab.vue';

export default {
  name: 'app',
  data() {
    return {
      msg: 'What Would Dolly Do?',
      colours: 7,
      isActive: false,
      current_colour: ''
    }
  },
  methods: {
    getRandomNumber: function( arrayName ) {
      return Math.floor( Math.random()*( arrayName.length ) );
    },
    getRandomColour: function( arrayName ) {
      let index = this.getRandomNumber( this.background_colours );
      this.current_colour = this.background_colours[index];
    },
  },
  computed: {
    background_colours: function() {
      let bg_array = [];

      for (var i = 1; i <= this.colours; i++) {
        bg_array.push( `background_${i}` );
      }

      return bg_array;
    }
  },
  mounted: function() {
    this.getRandomColour();
  },
  components: {
    Lorem,
    Quotes,
    Tabs,
    Tab
  },
}
</script>

<style lang="scss">
@import './assets/styles/_global.scss';

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: black;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  margin: 0;
}

.app {
  background-color: $pink;
  background: url('../src/assets/img/dolly-parton.png') no-repeat left fixed;
  background-size: cover;
}

header {
  padding: 0 $gutter;
  width: 100%;
}

.card {
  font-family: $cursive;
  border: 10px solid white;
  box-shadow: 5px 5px 8px rgba(15, 15, 15, .15);
  margin: 0 5% 32px auto;
  transform: rotate(-6deg);

  @media (min-width: $tablet-portrait) {
    font-size: 70px;
    width: 700px;
  }
}

.tab-container {
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  width: 100%;

  @media (min-width: $tablet-portrait) {
    flex-direction: row;
    justify-content: space-between;
  }

  .tabs {
    min-width: 15%;
  }
}

.content {
  display: flex;
  flex-direction: row;
  min-height: 70vh;
  padding: $gutter;
  width: 100%;

  @media (min-width: $tablet-portrait) {
    margin-top: $gutter * 2;
  }
}

//////// ABOUT SECTION
// Reset button default styles.
button {
  background: none repeat scroll 0 0 transparent;
  border-spacing: 0;
  border: medium none;
  display: inline-block;
  font-size: 20px;
  font-weight: normal;
  margin: 0;
  padding: 0;
  text-align: left;
  text-decoration: none;
  text-indent: 0;
}

// About section 'dropdown'.
.about-drop {
  background: $blue;
  bottom: 100%;
  font-family: $serif;
  height: 100vh;
  left: 0;
  padding: $gutter*2 $gutter;
  position: absolute;
  transition: bottom 0.4s ease-in-out;
  width: 100%;
  z-index: 1;

  // When open...
  &.active {
    bottom: 0;

    // Change those lines.
    .mobile-menu-bar:nth-of-type(1) {
      transform: translateY(12px) rotate(45deg);
    }

    .mobile-menu-bar:nth-of-type(2) {
      opacity: 0;
    }

    .mobile-menu-bar:nth-of-type(3) {
      transform: translateY(-12px) rotate(-45deg);
    }
  } // &.active

  // WWDD title.
  h2 {
    border-bottom: 2px solid $black;
    font-size: 34px;
    margin-top: 50px;

    @media (min-width: $tablet-portrait) {
      margin-top: 0;
    }
  }

  // Content.
  p {
    font-size: 24px;
    margin: 0;
  }
} // .about-drop


.about-drop {

  // Wrapper around content of about 'dropdown'.
  .wrapper {

    @media (min-width: $tablet-portrait) {
      padding: 10% 15%;
    }

    // Heart + link.
    a,
    .fa {
      color: $darkpink;
    }

    // Links.
    a {
      box-shadow: inset 0 -0.1em 0 -.5px $darkpink;
      -webkit-box-shadow: inset 0 -0.1em 0 -.5px $darkpink;

      color: $black;
      text-decoration: none;
      transition-duration: 0.2s;
      transition-property: box-shadow;
      transition-timing-function: cubic-bezier(0, 0, 0.58, 1);

      @media (min-width: $phone-landscape) {
        box-shadow: inset 0 -0.1em 0 0 $darkpink;
      }

      &:hover,
      &:focus,
      &:active {
        box-shadow: inset 0 -0.25em 0 -.5px $darkpink;
      }
    }
  } // .wrapper
} // .about-drop

// Open + Close About 'dropdown'.
.about-button {
  position: relative;
  z-index: 10;

  // When open...
  &.active {
    bottom: 0;

    // Change those lines.
    .mobile-menu-bar:nth-of-type(1) {
      transform: translateY(12px) rotate(45deg);
    }

    .mobile-menu-bar:nth-of-type(2) {
      opacity: 0;
    }

    .mobile-menu-bar:nth-of-type(3) {
      transform: translateY(-12px) rotate(-45deg);
    }
  }

  // Global styles for Hamburger Lines.
  .mobile-menu-bar {
    background-color: $black;
    display: block;
    height: 5px;
    margin: 7px auto;
    transition: transform 0.3s ease-in-out, opacity 0.3s ease-in-out;
    width: 40px;
  }
} // .about-button
</style>
