<template>
  <div id="app">
    <header class="site-header">
      Infinite Scroll Demo
    </header>
    <InfiniteScroll class="infinite-scroll-container" :current-index="currentPage" :last-index="lastPage" @update="loadMoreData">
        <transition-group name="list" class="grid-container">
          <Card v-for="item in list" :item="item" :key="item"></Card>
        </transition-group>
    </InfiniteScroll>
    <footer class="site-footer">
      End of Infinite Scroll Demo
    </footer>
  </div>
</template>

<script>
import InfiniteScroll from './components/InfiniteScroll/InfiniteScroll.vue'
import Card from './components/Card/Card.vue'
import Data from './Data/data.js'

export default {
  name: 'App',
  components: {
    InfiniteScroll,
    Card
  },
  data: function() {
    return {
        list: [],
        currentIndex: 0,
        lastIndex: 0,
    }
  },
  methods: {
    setUpInitialData() {
        this.list = Data.items[0]
        this.currentPage = 0
        this.lastPage = Data.items.length - 1
    },
    loadMoreData() {
        if(this.currentPage < this.lastPage) {
          this.currentPage++
          this.list.push(...Data.items[this.currentPage])
        }
    }
  },
  mounted() {
    this.setUpInitialData()
  }
}
</script>

<style>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 30px;
}
.list-enter-active, .list-leave-active {
  transition: all 1.5s;
}
.list-enter, .list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.site-header {
  background-color: #42b983;
  color: #fff;
  padding: 20px;
  margin-bottom: 30px;
  text-align: center;
  font-size: 30px;
}
.site-footer {
  background-color: black;
  color: #fff;
  padding: 20px;
  margin-top: 30px;
  text-align: center;
  font-size: 30px;
}
</style>
