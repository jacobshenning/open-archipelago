<template>
  <div>
    <section
      class="hero"
      :style="{
        backgroundColor: framework.color
      }"
    >
      <div class="hero-body">
        <div class="container">
          <h1 class="title is-1" :style="{ color: framework.contrastColor }">
            {{ framework.name }}
          </h1>
          <h2 class="subtitle" :style="{ color: framework.contrastColor }">
            {{ framework.description }}
          </h2>
          <div v-if="framework">
            <github-button
              :href="framework.repo_owner"
              data-size="large"
              data-show-count="true"
              aria-label="Follow @laravel on GitHub"
            >
              Follow @laravel
            </github-button>
            <github-button
              :href="framework.repository_html + `/subscription`"
              data-icon="octicon-eye"
              data-size="large"
              data-show-count="true"
              aria-label="Watch laravel/laravel on GitHub"
            >
              Watch
            </github-button>
            <github-button
              :href="framework.repository_html"
              data-icon="octicon-star"
              data-size="large"
              data-show-count="true"
              aria-label="Star on GitHub"
            >
              Star
            </github-button>
          </div>
        </div>
      </div>
    </section>
    <div class="container">
      <br />
      <div class="columns">
        <div class="column is-two-thirds">
          <h3 class="title is-3">Releases</h3>
          <div class="card">
            <div
              v-for="release in releases"
              :key="release.id"
              style="padding: 20px"
            >
              <a :href="release.html_url" target="_blank" class="title is-5">
                Release: {{ release.tag_name }}
              </a>
              <p>{{ release.created_at }}</p>
              <markdown-it-vue :content="release.body" />
              <hr />
            </div>
          </div>
        </div>
        <div class="column is-one-third">
          <h3 class="title is-3">Tweets</h3>
          <div class="card" style="padding: 0;">
            <a
              v-if="framework.twitter"
              class="twitter-timeline"
              data-theme="light"
              :href="framework.twitter"
            >
              Tweets
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios-https-proxy-fix'
import GithubButton from 'vue-github-button'
import MarkdownItVue from 'markdown-it-vue'

export default {
  components: {
    GithubButton,
    MarkdownItVue
  },
  data() {
    return {
      framework: {
        name: '',
        description: '',
        color: '',
        contrastColor: '',
        posts: []
      },
      releases: {}
    }
  },
  beforeCreate() {
    axios.get(`/${this.$route.params.slug}.json`).then((response) => {
      this.framework = response.data
      this.getReleases()
      this.loadTweets()
      this.loadBlogs()
    })
  },
  methods: {
    getReleases() {
      axios.get(`${this.framework.releases}`).then((response) => {
        this.releases = response.data
      })
    },
    loadTweets() {
      const recaptchaScript = document.createElement('script')
      recaptchaScript.setAttribute(
        'src',
        'https://platform.twitter.com/widgets.js'
      )
      document.head.appendChild(recaptchaScript)
    },
    loadBlogs() {}
  },
  xmlToJson(xml) {
    let obj = {}
    if (xml.nodeType === 1) {
      if (xml.attributes.length > 0) {
        obj['@attributes'] = {}
        for (let j = 0; j < xml.attributes.length; j++) {
          const attribute = xml.attributes.item(j)
          obj['@attributes'][attribute.nodeName] = attribute.nodeValue
        }
      }
    } else if (xml.nodeType === 3) {
      obj = xml.nodeValue
    }
    if (xml.hasChildNodes()) {
      for (let i = 0; i < xml.childNodes.length; i++) {
        const item = xml.childNodes.item(i)
        const nodeName = item.nodeName
        if (typeof obj[nodeName] === 'undefined') {
          obj[nodeName] = this.xmlToJson(item)
        } else {
          if (typeof obj[nodeName].push === 'undefined') {
            const old = obj[nodeName]
            obj[nodeName] = []
            obj[nodeName].push(old)
          }
          obj[nodeName].push(this.xmlToJson(item))
        }
      }
    }
    return obj
  }
}
</script>
