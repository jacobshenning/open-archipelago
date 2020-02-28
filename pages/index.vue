<template>
  <section class="section">
    <section class="hero">
      <div class="hero-body">
        <div class="container columns">
          <div>
            <img src="~/assets/logo2.png" style="max-height: 150px;" />
          </div>
          <div class="column">
            <br />
            <h1 class="title is-1">
              Open Archipelago
            </h1>
            <h2 class="subtitle">
              A way to keep up with many of the popular open-source frameworks
            </h2>
          </div>
        </div>
      </div>
    </section>
    <br />
    <br />
    <div class="tile is-ancestor">
      <nuxt-link class="tile is-parent" to="/laravel">
        <article
          class="tile is-child notification is-primary"
          style="backgroundColor: #ff2d20"
        >
          <p class="title">Laravel</p>
          <p class="subtitle">Laravel is a framework for web artisans</p>
        </article>
      </nuxt-link>
      <nuxt-link class="tile is-parent" to="/vue">
        <article
          class="tile is-child notification is-info"
          style="backgroundColor: #42b983"
        >
          <p class="title">Vue</p>
          <p class="subtitle">Vue is a frontend framework</p>
        </article>
      </nuxt-link>
    </div>
  </section>
</template>

<script>
export default {
  components: {}
}
</script>
