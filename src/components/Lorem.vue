<template>
  <div class="hello">
    <form class="settings" @submit.prevent>
        <span>
          <label for="numPara">How many paragraphs?</label>
          <input id="numPara" type="number" min="1" inputmode="numeric" pattern="[0-9]*" v-model.number="numPara">
        </span>

        <span>
          <label for="minLength">Minimum paragraph length:</label>
          <input id="minLength" type="number" min="1" inputmode="numeric" pattern="[0-9]*" v-model.number="minLength"></input>
        </span>

        <span>
          <label for="maxLength">Maximum Paragraph Length:</label>
          <input id="maxLength" type="number" min="1" inputmode="numeric" pattern="[0-9]*" v-model.number="maxLength"></input>
        </span>
      </form>
    <div class="results">
      <p v-for="lyric in ipsum">{{ lyric }}</p>
    </div>
  </div>
</template>


<script>
import lyrics from "../lyrics.js";

export default {
  name: 'Lorem',
  data() {
    return {
      lyrics,
      numPara: 2,
      minLength: 3,
      maxLength: 8,
    };
  },
  computed: {
    ipsum () {
      // Returns lorem ipsum results.
      let newLyricsArray = [];

      // Add generated ipsum.
      for ( var i = 0; i < this.numPara; i++ ) {
        const sortedLyrics = this.shuffle( this.lyrics );
        const sentenceCount = this.randomNumber();

        let tempArray = [];

        for ( var x = 0; x < sentenceCount; x++ ) {
          tempArray.push( sortedLyrics[x] );
        }

          newLyricsArray.push( tempArray.join( '. ' ) );
      }

      return newLyricsArray;
    }
  },
  methods: {
    shuffle( array ) {
      for (let i = array.length - 1; i > 0; i--) {
          const j = Math.floor(Math.random() * (i + 1));
          [array[i], array[j]] = [array[j], array[i]]; // eslint-disable-line no-param-reassign
      }
      return array;
    },
    randomNumber() {
        return Math.floor( Math.random() * ( this.maxLength - this.minLength + 1 ) ) + this.minLength;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../assets/styles/_global.scss';

a {
  color: $darkpink;
}

form {
  span {
    display: block;
    margin-bottom: $gutter / 2;
  }

  label {
    display: inline-block;
    font-family: $sans;
    font-size: 22px;
    margin-right: $gutter;
    min-width: 295px;
  }

  input {
    border-radius: 2px;
    border: 1px solid $darkpink;
    box-shadow: inset 1px 1px 3px $darkpink;
    box-sizing: border-box;
    max-width: 100%;
    padding: 0.5em 0.6em;
    vertical-align: middle;
  }
} // form

.results {
  border: 2px solid rgba($black, 0.3);
  font-family: $serif;
  font-size: 24px;
  margin-top: $gutter;
  max-height: 35vh;
  overflow-y: auto;
  padding: $gutter / 2 $gutter;

  p {
    margin: 0 0 $gutter;

    &:last-of-type {
      margin: 0;
    }
  } // p
} // .results

// Vertical Scroll bar.
::-webkit-scrollbar {
    -webkit-appearance: none;
}

::-webkit-scrollbar:vertical {
    width: 11px;
}

::-webkit-scrollbar:horizontal {
    height: 11px;
}

::-webkit-scrollbar-thumb {
    background-color: rgba(0, 0, 0, .3);
    border-radius: 8px;
}
</style>
