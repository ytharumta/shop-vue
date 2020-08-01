<template>
  <div class="product">
    <Header />
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="breadcrumb-text product-more text-left">
              <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
              <span>Detail</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
      <div class="container">
        <div class="row">
          <div class="col-lg-12">
            <div class="row">
              <div class="col-lg-6">
                <div class="product-pic-zoom">
                  <img class="product-big-img" :src="default_picture" alt="" />
                </div>
                <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                  <carousel :nav="false" :dots="false" :autoplay="false" class="product-thumbs-track ps-slider">

                    <div class="pt" v-for="ss in productDetails.galleries" :key="ss.id" @click="changeImage(ss.photo)" :class="ss.photo == default_picture ? 'active' : ''">
                      <img :src="ss.photo" alt="" />
                    </div>

                  </carousel>
                </div>
              </div>
              <div class="col-lg-6">
                <div class="product-details">
                  <div class="pd-title text-left">
                    <span>{{productDetails.type}}</span>
                    <h3>{{productDetails.name}}</h3>
                  </div>
                  <div class="pd-desc text-left">
                    {{productDetails.description}}
                    <h4>${{productDetails.price}}</h4>
                  </div>
                  <div class="quantity">
                    <router-link to = '/cart' class="primary-btn pd-cart">
                      Add to Cart
                    </router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Product Shop Section End -->
    <RelatedProduct/>
    <FooterHome />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Header from "@/components/Header.vue";
import FooterHome from "@/components/FooterHome.vue";
import RelatedProduct from "@/components/RelatedProduct.vue";
import carousel from 'vue-owl-carousel';
import axios from 'axios';
export default {
  name: "product",
  components: {
    Header,
    FooterHome,
    carousel,
    RelatedProduct,
  },
  data(){
      return{
          default_picture: "",
          thumbs: [
              "img/mickey1.jpg",
              "img/mickey2.jpg",
              "img/mickey3.jpg",
              "img/mickey4.jpg",
          ],
          productDetails: [],
      }
  },
  methods:{
      changeImage(urlImage){
          this.default_picture = urlImage;
      },
      setDataPicture(data){
        this.productDetails = data;
        this.default_picture = data.galleries[0].photo;
      }
  },
  mounted(){
    axios
    .get('http://shayna-backend.belajarkoding.com/api/products', {
      params: {
        id: this.$route.params.id
      }
    })
    .then(res => (this.setDataPicture(res.data.data)))
    .catch(err => console.log(err));
  }

};
</script>

<style scoped>
    .product-thumbs .pt{
        margin-right: 10px;
    }
</style>