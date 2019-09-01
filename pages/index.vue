<template>
  <div ref="page">
    <Console />
    <Header 
      :title="header.title"
      :navitems="header.navitems"
      :img="header.img"
    />
    <main ref="main">
      <Description
        v-for="item of midSection" 
        :key="midSection.indexOf(item)"
        :title="item.description.title"
        :text="'bjhdshfdshjf'"
        :img="'dfhdshfdsh'"  
        :slug="item.description.slug"/>
      <section id="registration" aria-label="aanmelden">
        <Form :title="formTitle" />
      </section>
    </main>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import Form from '~/components/Form.vue'
import Header from '~/components/Header.vue'
import Description from '~/components/Description.vue'
import Console from '~/components/Console.vue'

export default {
  components: {
    Logo,
    Form,
    Header,
    Description,
    Console,
  },

  async asyncData({ params })  {
    let md = await import('~/content/index.md')

    return {
      formTitle: md.attributes['form-title'],
      midSection: md.attributes['mid-section'],
      header: { 
        ... md.attributes['header'], 
        navitems: md.attributes['mid-section'].map((midSectionItem) => {
          return midSectionItem.description
        })
      }
    }
  },

  head() {
    return {
      title: this.header.title,
      meta: [
        //add image meta tag since header image is implemented with a CSS tag
        { hid: 'meta-image', name: 'og:image', property: 'og:image', content: this.header.img },
        { hid: 'description', name: 'description', content: 'My custom description' },
      ]
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  max-width: 100vw;
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
