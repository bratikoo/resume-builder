<template>
  <div class="container column">
    <resume-form @add-block="addBlock"></resume-form>
    <resume-view :blocks="blocks"></resume-view>

  </div>
  <div class="container">
    <app-loader v-if="loading"></app-loader>
    <resume-comments
      v-else
      :comments="comments"
      @load-comments="loadComments"
      >
    </resume-comments>
  </div>
</template>

<script>
import ResumeForm from './components/ResumeForm'
import ResumeView from './components/ResumeView'
import ResumeComments from './components/ResumeComments'
import AppLoader from './components/AppLoader'

export default {
  data () {
    return {
      blocks: [],
      comments: [],
      loading: false
    }
  },
  methods: {
    addBlock (block) {
      this.blocks.push(block)
    },
    async loadComments () {
      try {
        this.loading = true
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
        this.comments = await response.json()
        this.loading = false
      } catch (e) {

      }
    }
  },
  components: {
    ResumeForm,
    ResumeView,
    ResumeComments,
    AppLoader
  }
}
</script>

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
