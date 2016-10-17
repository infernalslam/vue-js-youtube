<template>
  <div id="app">
    <iframe width="420" height="315" :src="videoId" frameborder="0" allowfullscreen></iframe> <br>
    Search : => <input type="text" v-model="keyword"> <button @click="search(keyword)">ค้นหา</button>
    <div v-for="show in list">
      <img :src="show.snippet.thumbnails.medium.url" @click="select(show.id.videoId)">
      {{show.snippet.title}} <br>
      {{show.snippet.description}} <br>
      {{show.snippet.channelTitle}} <br>
      <hr>
    </div>
  </div>
</template>

<script>
export default {
  components: {
  },
  data () {
    return {
      videoId: 'https://www.youtube.com/embed/UqyT8IEBkvY?autoplay=1',
      keyword: '',
      list: []
    }
  },
  methods: {
    search: function (keyword) {
      var vm = this
      this.$http.get('http://localhost:3000/search?keyword=' + keyword).then(function (res) {
        vm.list = JSON.parse(res.body).items
        console.log(vm.list)
      })
    },
    select: function (id) {
      console.log(id)
      this.videoId = `https://www.youtube.com/embed/${id}?autoplay=1`
    }
  }
}
</script>
