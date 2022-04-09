<template>
  <div class="bg-white sticky-top">
    <div class="container">
      <nav class="navbar px-0 navbar-expand-lg navbar-light bg-white">
        <router-link
          to="/"
          class="navbar-brand position-absolute"
          style="left: 50%; transform: translate(-50%, -50%); top: 50%"
        >
          Navbar
        </router-link>

        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div
          class="collapse navbar-collapse bg-white custom-header-md-open"
          id="navbarNav"
        >
          <ul class="navbar-nav">
            <li class="nav-item active">
              <router-link class="nav-link" to="/products"
                >產品頁面</router-link
              >
            </li>
          </ul>
        </div>
        <div class="d-flex">
          <router-link to="/CartView"></router-link>
          <a href="#" class="position-relative px-1">
            <i class="bi bi-bag fs-5"></i>
            <span
              class="
                position-absolute
                top-0
                start-100
                translate-middle
                badge
                rounded-pill
                bg-danger
              "
            >
              {{ cartData?.carts?.length }}
              <span class="visually-hidden">unread messages</span>
            </span>
          </a>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
import emitter from '@/utils/emitter'

export default {
  data () {
    return {
      cartData: {
        carts: []
      }
    }
  },
  // 取得單一特定產品資訊
  methods: {
    getCart () {
      const url = `${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/cart`
      this.$http.get(url).then((res) => {
        console.log('getCart:', res)
        this.cartData = res.data.data
      })
    }
  },
  mounted () {
    this.getCart()
    emitter.on('get-cart', () => {
      this.getCart()
    })
  }
}
</script>
