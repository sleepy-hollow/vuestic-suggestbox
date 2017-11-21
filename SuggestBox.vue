<template>
  <div class="suggest-box">
    <div class="form-group with-icon-right dropdown select-form-group"
        style="position:relative" 
        v-bind:class="{'show':openSuggestion}">
      <div class="input-group">
        <input class="input-width" type="text" :value="value" @input="updateValue($event.target.value)"
          @keydown.enter = 'enter'
          @keydown.down = 'down'
          @keydown.up = 'up'>
      </div>
      <div class="dropdown-menu">
        <div class="dropdown-menu-content">
          <div class="dropdown-item" v-for="(suggestion, index) in matches"
              v-bind:class="{'active': isActive(index+1)}"
              @click="suggestionClick(index+1)">
            <a href="#">{{ suggestion.name }}</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true
    },
    suggestions: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      open: false,
      current: 0
    }
  },
  computed: {
    // Filtering the suggestion based on the input
    matches () {
      return this.suggestions.filter((obj) => {
        return obj.name.indexOf(this.value) >= 0
      }).splice(0, 20)
    },
    openSuggestion () {
      return this.matches.length !== 0 && this.open === true
    }
  },
  methods: {
    updateValue (value) {
      if (this.open === false) {
        this.open = true
        this.current = 0
      }
      this.$emit('input', value)
    },
    // When enter pressed on the input
    enter () {
      if (this.current !== 0) {
        this.$emit('input', this.matches[this.current - 1].name)
        this.current = 0
        this.open = false
      }
    },
    // When up pressed while suggestions are open
    up () {
      if (this.current > 0) {
        this.current--
      }
    },
    // When up pressed while suggestions are open
    down () {
      if (this.current < this.matches.length && this.open === true) {
        this.current++
      }
    },
    // For highlighting element
    isActive (index) {
      return index === this.current
    },
    // When one of the suggestion is clicked
    suggestionClick (index) {
      this.$emit('input', this.matches[index - 1].name)
      this.open = false
    }
  }
}
</script>

<style lang="scss">
  .suggest-box {
    .select-form-group {
      .dropdown-menu {
        padding: 0;
      }
    }

    .form-group {
      border-style: groove;
    }

    .dropdown-menu .dropdown-menu-content {
      background-color: #FFFFFF;
      box-shadow: 0 4px 9.6px 0.4px black;
    }

    a {
      color: black;
    }

    .dropdown-item.active, .dropdown-item:active {
      background-color: #6eed78;
    }

    .dropdown-item:focus, .dropdown-item:hover {
      background-color: #6eed78;
    }
  }
</style>
