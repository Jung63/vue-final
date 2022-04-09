<template>
  <div class="container mt-md-5 mt-3 mb-7">
    <div class="row row-cols-1 row-cols-md-2 row-cols-lg-3">
      <!-- row 透過外層決定內層欄數 前為行動版 後為桌面板-->
      <div class="col" v-for="product in products" :key="product.id">
        <!-- 內層不決定寬度 -->
        <div class="card border-0 mb-4 position-relative position-relative">
          <!-- 背景圖 -->
          <div
            :style="{ backgroundImage: `url(${product.imageUrl})` }"
            style="
              height: 300px;
              background-size: cover;
              background-position: center;
            "
          ></div>

          <a href="#" class="text-dark">
            <i
              class="far fa-heart position-absolute"
              style="right: 16px; top: 16px"
            ></i>
          </a>
          <div class="card-body p-0">
            <h4 class="mb-0 mt-3">
              <router-link :to="`/product/${product.id}`">{{
                product.title
              }}</router-link>
            </h4>
            <p
              class="card-text text-muted mb-0"
              style="height: 4.5rem; overflow: hidden"
            >
              {{ product.description }}
            </p>
            <p class="text-muted mt-3">NT ${{ product.price }}</p>
          </div>
        </div>
      </div>
    </div>
    <nav class="d-flex justify-content-center">
      <ul class="pagination">
        <li class="page-item">
          <a class="page-link" href="#" aria-label="Previous">
            <span aria-hidden="true">&laquo;</span>
          </a>
        </li>
        <li class="page-item active"><a class="page-link" href="#">1</a></li>
        <li class="page-item"><a class="page-link" href="#">2</a></li>
        <li class="page-item"><a class="page-link" href="#">3</a></li>
        <li class="page-item">
          <a class="page-link" href="#" aria-label="Next">
            <span aria-hidden="true">&raquo;</span>
          </a>
        </li>
      </ul>
    </nav>
  </div>
</template>

<script>
export default {
  data () {
    return {
      products: []
    }
  },
  methods: {
    getProducts () {
      const url = `${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/products/all`
      this.$http.get(url).then((res) => {
        this.products = res.data.products
      })
    }
  },
  mounted () {
    this.getProducts()
  }
}
</script>
