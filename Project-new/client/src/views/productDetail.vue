<template>
<!-- eslint-disable-next-line -->
<!-- eslint-disable  -->
<main class="mt-3">
    <div class="container">
      <div class="row">
        <div class="col-md-5">
          <div id="carouselExampleIndicators" class="carousel carousel-dark slide" data-bs-ride="carousel">
            <ol class="carousel-indicators">
              <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active"></li>
              <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1"></li>
              <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2"></li>
            </ol>
            <div class="carousel-inner">
              <div :class="`carousel-item ${i == 0?'active':''}`" :key="i" v-for="(img, i) in productImage">
                <img :src="`/download/${productId}/${img.path}`" class="d-block w-100" alt="...">
              </div>              
            </div>
            <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Previous</span>
            </a>
            <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Next</span>
            </a>
          </div>
        </div>
        <div class="col-md-7">
          <div class="card shadow-sm">
            <div class="card-body">
              <h5 class="card-title">{{ productDetail.product_name }}</h5>
              <h5 class="card-title pt-3 pb-3 border-top">{{getCurrencyFormat(productDetail.product_price)}}원</h5>
              <p class="card-text border-top pt-3">
                <span class="badge bg-dark me-1">{{  productDetail.category1  }}</span>
                <span class="badge bg-dark me-1">{{  productDetail.category2  }}</span>
                <span class="badge bg-dark">{{  productDetail.category3  }}</span>
              </p>
              <p class="card-text pb-3">
              배송비 {{getCurrencyFormat(productDetail.delivery_price)}}원 | 도서산간(제주도) 배송비 추가 {{ getCurrencyFormat(productDetail.add_delivery_price) }} 원 | 택배배송 | {{productDetail.outbound_days}}일 이내 출고 (주말,공휴일 제외)
              </p>
              <p class="card-text border-top pb-3">
                <div class="row  pt-3">
                  <div class="col-auto">
                    <label class="col-form-label">구매수량</label>
                  </div>
                  <div class="col-auto">
                    <div class="input-group">
                      <span class="input-group-text" style="cursor: pointer;" @click="minus()">-</span>
                      <input type="text" class="form-control" style="width:50px;" v-model="count">
                      <span class="input-group-text" style="cursor: pointer;" @click="plus()">+</span>
                    </div>
                  </div>
                </div>
              </p>
              <div class="row pt-3 pb-3 border-top">
                <div class="col-6">
                  <h3>총 상품 금액</h3>
                </div>
                <div class="col-6" style="text-align: right;">
                  <h3>{{getCurrencyFormat(totalPrice)}}원</h3>
                </div>
              </div>
              <div class="d-flex justify-content-between align-items-center">
                <div class="col-6 d-grid p-1">
                  <button type="button" class="btn btn-lg btn-dark">장바구니 담기</button>
                </div>
                <div class="col-6 d-grid p-1">
                  <button type="button" class="btn btn-lg btn-danger">주문하기</button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <img :src="`/download/${productId}/${productDetail.path}`" class="img-fluid" />
        </div>
      </div>
    </div>
  </main>
</template>
<script>
// eslint-disable-next-line
/* eslint-disable */
export default {
  data () {
    return {
	  count: 0,
	  totalPrice: 0,
	  productId: 0,
    productDetail: {},
    productImage: []
    }
  },
  created () {
    this.productId = this.$route.query.product_id
    this.getProductDetail()
    this.getProductImage()
  }, 
  methods: {
    getCurrencyFormat (value){
      return this.$currencyFormat(value)
    },
    async getProductDetail () {
      let productDetail = await this.$api('/api/productDetail', { param: [this.productId] })
	  if(productDetail.length > 0 ) {
		this.productDetail = productDetail[0];
	  }
      console.log('this.productDetail',this.productDetail)
    },
    async getProductImage () {
      this.productImage = await this.$api('/api/productMainImages', { param: [this.productId] })
      console.log('this.productImage', this.productImage)
    },
    plus() {
    this.count = this.count + 1;	
    this.totalPrice = (this.productDetail.product_price * this.count) + this.productDetail.delivery_price;
    },
    minus() {
      if(this.count <= 1) {
        return;
      }else {
      this.count = this.count - 1;
      this.totalPrice = (this.productDetail.product_price * this.count) + this.productDetail.delivery_price;
      }
	  }
  }
}
</script>