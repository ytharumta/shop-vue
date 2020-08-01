<template>
  <div class="home">
    <Header />
    <CarouselHome/>
    <ItemHome/>
    <InstaHome/>
    <PartnerHome/>
    <FooterHome/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Header from "@/components/Header.vue";
import CarouselHome from "@/components/CarouselHome.vue";
import ItemHome from "@/components/ItemHome.vue";
import InstaHome from "@/components/InstaHome.vue";
import PartnerHome from "@/components/PartnerHome.vue";
import FooterHome from "@/components/FooterHome.vue";

export default {
  name: "Home",
  components: {
    Header,
    CarouselHome,
    ItemHome,
    InstaHome,
    PartnerHome,
    FooterHome,
  },
};
</script>
