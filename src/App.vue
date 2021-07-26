<template>
  <div>
    <search-form />
  </div>
</template>

<script>
import SearchForm from './components/search-form.vue'

export default {
  name: 'App',

  components: {
    SearchForm,
  }
}
</script>


<style>
/* Box sizing rules */
*,
*::before,
*::after {
  box-sizing: border-box;
}

/* Remove default margin */
body,
h1,
h2,
h3,
h4,
p,
ul,
ol,
li,
figure,
figcaption,
blockquote,
fieldset,
dl,
dd {
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Roboto', sans-serif;
}

button,
fieldset {
  outline: none;
  border: none;
}

.row {
  display: flex;
  flex: 1;
}

</style>
