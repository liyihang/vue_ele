 <template>
  <div id="app">
    <v-header></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>

    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import header from './components/header/header'
import goods from './components/goods/goods'
import ratings from './components/ratings/ratings'
import seller from './components/seller/seller'
export default {
  components: {
    'v-header': header,
    goods,
    ratings,
    seller
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#app .tab {
  display: flex;
  widows: 100%;
  height: 40px;
  line-height: 40px;
}
.tab .tab-item {
  flex: 1;
  text-align: center;
}
</style>
