<template>
  <div id="disqus_thread"></div>
</template>

<script>
export default {
  props: {
    permalink: {
      type: String,
      required: true
    },
    shortname: {
      type: String,
      required: true
    }
  },

  mounted() {
    const { permalink } = this
    window.disqus_config = function() {
      this.page.url = permalink
      this.page.identifier = permalink
    }
    const script = document.createElement('script')
    script.async = true
    script.src = `https://${
      this.shortname
    }.disqus.com/embed.js`
    script.setAttribute('data-timestamp', +new Date())
    document.body.appendChild(script)
  }
}
</script>
