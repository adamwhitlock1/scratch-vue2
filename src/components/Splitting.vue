<template>
  <div id="app">
    <span v-for="(word, wordIndex) in sentenceData" :key="wordIndex" :class="getWordClassName(wordIndex)">

      <span v-for="(letter, letterIndex) in word.letters"
      :key="`${letter}${letterIndex}`"
      :class="getCharacterClassName(letterIndex, word.startingNumber)">{{letter}}</span>

      <span v-if="word !== words.at(-1)" class="whitespace">&nbsp;</span>

    </span>

    <pre v-if="debug">{{ JSON.stringify(sentenceData, null, 2) }}</pre>
  </div>
</template>

<script>
export default {
  name: 'Splitting',
  props: {
    sentence: {
      type: String,
      required: true
    },
    wordClassName: {
      type: String,
      default: 'word'
    },
    characterClassName: {
      type: String,
      default: 'char'
    },
    sequential: {
      type: Boolean,
      default: true
    },
    debug: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    getCharacterClassName(letterIndex, startingNumber) {
      const indexValue = this.sequential ? (letterIndex + startingNumber) : letterIndex
      return `${this.characterClassName} ${this.characterClassName}__index-${indexValue}`
    },
    getWordClassName(wordIndex) {
      return `${this.wordClassName} ${this.wordClassName}__index-${wordIndex}`
    }
  },
  computed: {
    words() {
      return this.sentence.split(" ")
    },
    sentenceData() {
        return this.words.reduce((accumulator, current) => {
          // the number that the last word 'left off at'
          const startingNumber = accumulator.reduce((total, currentObj) => {
          total = total + ((currentObj?.wordLength) || 0)
          return total
          }, 0)

          accumulator.push({word: current, wordLength: current.length, startingNumber, letters: Array.from(current) })

          return accumulator
        }, [])
      }
    }
}
</script>
