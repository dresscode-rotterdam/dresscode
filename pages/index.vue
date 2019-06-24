<template>
  <main>
    <Console />
    <Header />
       <Description
                 
                 :title="this.content.attributes.['mid-section'][0].description.title" 
                 :text="'bjhdshfdshjf'"
                 :img="'dfhdshfdsh'"  />
    <section id="registration" aria-label="aanmelden">
      <Form :title="'gdhjdghejd'" />
    </section>
  </main>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Form from '~/components/Form.vue'
import Header from '~/components/Header.vue'
import Description from '~/components/Description.vue'
import Console from '~/components/Console.vue'
import md from '~/content/index.md'

export default {
  components: {
    Logo,
    Form,
    Header,
    Description,
    Console,
  },

  data() {
    return {
      content: md
    }
  },

  mounted() {
    console.log(this.content.attributes['mid-section'])
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
  @apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  max-width: 100vw;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 4em;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

#registration {
  display: flex;
  justify-content: center;
  padding: 32px; 
}
</style>
