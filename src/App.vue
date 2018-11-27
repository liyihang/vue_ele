 <template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">
          <div class="item">商品</div>
        </router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">
          <div class="item">评论</div>
        </router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">
          <div class="item">商家</div>
        </router-link>
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
const ERROR = 0
export default {
  data () {
    return {
      seller: {}
    }
  },
  created () {
    this.axios.get('/api/seller').then((response) => {
      response = response.data
      if (response.errno === ERROR) {
        this.seller = response.data
      }
    })
  },
  components: {
    'v-header': header,
    goods,
    ratings,
    seller
  }
}
</script>

<style>

#app .tab {
  display: flex;
  widows: 100%;
  height: 40px;
  line-height: 40px;
  border-bottom: 1px solid #ebebeb
}
.tab .tab-item {
  flex: 1;
  text-align: center;
}
.tab-item > a {
  display: block;
  font-family: simsun;
  font-size: 1rem;
  color: #666
}
.router-link-active .item{
  font-weight: 700;
  color: #ffe339;
}
</style>
