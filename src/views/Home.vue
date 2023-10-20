<template>
  <div>
    <section>
      <div class="container-fluid sectionFix bannersCont" >
        <div class="row bannersCont">
          <div class="col-lg-6 dark-overlay split-screen-column align-items-center align-items-lg-end" style="background-image: url(../assets/banner1.jpg); background-color: #d2cecb;"> 
          <!-- <div class="col-lg-6 dark-overlay split-screen-column align-items-center align-items-lg-end" style="background-image: url(../assets/backk1.jpg); background-color: #d2cecb;">  -->
            <div class="py-6 mt-6 overlay-content px-lg-5 mt-lg-0 mb-lg-5" style="margin: 0 auto !important">
              <h1 class="mb-2 text-white display-3 fw-bold split-screen-heading letter-spacing-1">STICKERS</h1>
              <router-link to="/products?category=STICKERS#!"><button class="catButton" type="button">VER PRODUCTOS</button></router-link>
            </div>
            
          </div>
          <div class="col-lg-6 split-screen-column align-items-center align-items-lg-end" style="background-image: url(../assets/banner2.jpg); background-color: #e5b6b4;"> 
          <!-- <div class="col-lg-6 split-screen-column align-items-center align-items-lg-end" style="background-image: url(../assets/backk2.jpg); background-color: #e5b6b4;">  -->
            <div class="py-6 px-lg-5 mb-lg-5" style="margin: 0 auto !important">
              <h1 class="mb-2 display-3 fw-bold split-screen-heading letter-spacing-1" style="color: white;">PARCHES TEXTILES</h1>
              <router-link to="/products?category=PARCHES#!"><button class="catButton" type="button">VER PRODUCTOS</button></router-link>
            </div>
          </div>
        </div>
      </div>
    </section>

    <div class="sectionTitle">
      <span>NUEVOS PRODUCTOS</span>
    </div>

    <section class="pb-2 " style="margin: 70px 0">
      <div class="container">
        <!-- <div class="row">
          <div class="mx-auto text-center col-xl-8">
            <h2 class="text-uppercase">NUEVOS PRODUCTOS</h2>
            <p class="lead text-muted">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
          </div>
        </div> -->

        <div class="row">
          <!-- product-->
          <div class="col-lg-3 col-md-4 col-6" v-for="item in fourProducts" >
            <router-link :to="/product/+item.slug">
              <div >
                <div class="product-image">
                  <div class="ribbon ribbon-info" v-if="item.discount">En oferta</div>
                  <img class="img-fluid" :src="$url+'/getImage/'+item.image" alt="product"/>
                  <div class="product-hover-overlay"><a class="product-hover-overlay-link" href="detail.html"></a>
                    <div class="product-hover-overlay-buttons"><a class="btn btn-dark btn-buy" href=""><span class="btn-buy-label ms-2">Ver más</span></a>
                    </div>
                  </div>
                </div>
                <div class="py-2">
                  <p class="mb-1 text-sm text-muted">{{item.category}}</p>
                  <h3 class="mb-1 h6 text-uppercase">
                    <a class="text-dark" href="detail.html">{{item.name}}</a>
                  </h3>
                  <span class="text-muted">{{ priceConverter(item.price) }} </span>
                </div>
              </div>
            </router-link>
          </div>
          <!-- /product-->
        </div>

      </div>
    </section>

    <div class="sectionTitle">
      <span>LO MAS VENDIDO</span>
    </div>
    
    <section class="py-4 bg-gray-100" style="margin: 70px 0">
      <div class="container">
        <!-- <div class="row">
          <div class="mx-auto mb-5 text-center col-xl-8">
            <h2>LO MAS VENDIDO</h2>
            <p class="lead text-muted">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
          </div>
        </div> -->

        <!-- <div class="row">
          <div class="mb-4 col-md-6 d-flex align-items-md-stretch mb-md-0">
            <div class="py-6 text-center text-white d-flex align-items-center dark-overlay w-100 py-md-0 model1img" style="">
             <a class="tile-link" href="category.html"> </a>
              <div class="card-img-overlay w-100 overlay-content">
                <h2 class="mb-0 display-2 fw-bold text-uppercase">UPTEMPO</h2>
              </div>
            </div>
          </div>
          <div class="col-md-6">
            <div class="mb-4 text-center text-white border-0 card dark-overlay">
              <img class="card-img" src="../assets/model3.jpeg" alt="Ladies"><a class="tile-link" href="category.html"> </a>
              <div class="card-img-overlay d-flex align-items-center">
                <div class="text-center w-100 overlay-content">
                  <h2 class="mb-0 text-center display-4 fw-bold text-uppercase">RETRO 4</h2>
                </div>
              </div>
            </div>
            <div class="text-center text-white border-0 card dark-overlay">
              <img class="card-img" src="../assets/model2.jpg" alt="Accessories"><a class="tile-link" href="category.html"> </a>
              <div class="card-img-overlay d-flex align-items-center">
                <div class="text-center w-100 overlay-content">
                  <h2 class="mb-0 text-center display-4 fw-bold text-uppercase">AIR MAX</h2>
                </div>
              </div>
            </div>
          </div>
        </div> -->

        <div class="row">
          <!-- product-->
          <div class="col-lg-3 col-md-4 col-6" v-for="item in fourProducts" >
            <router-link :to="/product/+item.slug">
              <div class="product">
                <div class="product-image">
                  <div class="ribbon ribbon-info" v-if="item.discount">En oferta</div>
                  <img class="img-fluid" :src="$url+'/getImage/'+item.image" alt="product"/>
                  <div class="product-hover-overlay"><a class="product-hover-overlay-link" href="detail.html"></a>
                    <div class="product-hover-overlay-buttons"><a class="btn btn-dark btn-buy" href=""><span class="btn-buy-label ms-2">Ver más</span></a>
                    </div>
                  </div>
                </div>
                <div class="py-2">
                  <p class="mb-1 text-sm text-muted">{{item.category}}</p>
                  <h3 class="mb-1 h6 text-uppercase">
                    <a class="text-dark" href="detail.html">{{item.name}}</a>
                  </h3>
                  <span class="text-muted">{{ priceConverter(item.price) }} </span>
                </div>
              </div>
            </router-link>
          </div>
          <!-- /product-->
        </div>

      </div>
    </section>

  </div>
</template>

<style>
  .model1img{
    background: center center url('../assets/model1.jpg') no-repeat; background-size: cover;
  }
  .product-image{
    display: block;
    position: relative;
    overflow: hidden;
    height: 320px;
  }
  .sectionFix{
    margin-top: 0px;
  }

  .sectionTitle {
    width: 100%; 
    padding-bottom:8px; 
    height: 100px; 
    background-color:black; 
    display:flex; 
    justify-content: center; 
    align-items: center;
  }

  .sectionTitle span {
    color:rgb(254, 75, 0); 
    font-size:40px; 
    font-weight:600;
  }

  @media (max-width:991px){
    .sectionFix{
      margin-top: 84px;
    }
    .bannersCont {
      height: calc(100vh - 91,38px);
    }
    .sectionTitle {
      padding-bottom:8px; 
      height: 70px; 
      padding-bottom: 4px;
    }
    .sectionTitle span {
      font-size:24px; 
      font-weight:600;
    }
  }
</style>

<script>
// @ is an alias to /src
import axios from 'axios'
import currencyFormatter from 'currency-formatter'
import { initCarousel } from '../../public/assets/js/theme.d7b4a888'
import carousel from 'vue-owl-carousel'

export default {
  name: 'Home',
  components: {
    carousel
  },
  data(){
    return {
      fourProducts: [],
      mostWantedProducts: [],
      freeShipping: ''
    }
  },
  mounted () {
  window.scrollTo(0, 0)
  },
  methods: {
    getFourProducts(){
      var loader = this.$loading.show({
        container: this.fullPage ? null : this.$refs.formContainer,
        canCancel: false,
        color: "orange",
        opacity: 1
      });
      axios.get(this.$url+'/public/getLatestProducts', {
        headers: {
          "Content-Type": 'application/json',
        }
        }).then((response) => {
          const {data} = response
          this.fourProducts = data
          loader.hide()
        }).catch( error => {
          this.msm_error = error.response.data.msg
          loader.hide()
        })
    },
    getMostWantedProducts(){
      axios.get(this.$url+'/public/getMostWantedProducts', {
            headers: {
              "Content-Type": 'application/json',
            }
            }).then((response) => {
              const {data} = response
              this.mostWantedProducts = data
            }).catch( error => {
              console.log(error.response.data.msg)
              this.msm_error = error.response.data.msg
               
            })
    },
    priceConverter(price){
        return currencyFormatter.format(price, { code: 'ARS' });

    },
  },
  beforeMount(){
    this.getFourProducts()
    this.getMostWantedProducts()
    initCarousel.init()
  }
}
</script>
