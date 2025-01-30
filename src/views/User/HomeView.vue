<template>
    <main-header />
    <section class="hero__section">
        <img 
            class="hero__image" 
            src="https://www.next.co.uk/cms/resource/blob/840444/91cfd22ecdcf5797673d4050efc1accb/200125-block1-hero-dt-live-amend-data.jpg" 
            alt="Hero Section Image"
        />
        <div class="container" style="text-align: center;">
            <div class="hero__text">
                <h4>Trade-in-offer</h4>
                <h3>Super value deals On all products</h3>
                <p style="color: aliceblue;">Save more with coupons & get up to 70% off!</p>
                <router-link to="/shop">
                    <action-button btnvalue="Shop Now" />
                </router-link>
            </div>
        </div>
    </section>
    <advert-section />
    <!-- <service-section /> -->
    <section class="feature__section">
        <div class="container">
            <featured-products :featuredProducts="featuredProducts" />
        </div>
    </section>

    <banner-section />
    <new-arrivals :newArrivals="newArrivals" />
    <news-letter />
    <main-footer />
</template>

<script>
import ServiceSection from "@/components/home_components/ServiceSection.vue";
import BannerSection from "@/components/home_components/BannerSection.vue";
import NewArrivals from "@/components/home_components/products/NewArrivals.vue";
import AdvertSection from "@/components/home_components/AdvertSection.vue";
import FeaturedProducts from "@/components/home_components/products/FeaturedProducts.vue";
import ActionButton from "@/components/ActionButton.vue";
import MainHeader from "@/components/MainHeader.vue";
import NewsLetter from "@/components/NewsLetter.vue";
import MainFooter from "@/components/MainFooter.vue";

import axios from "axios";
import { mapActions } from "vuex";

export default {
    name: "HomeView",
    data() {
        return {
            products: [],
        };
    },
    async created() {
        let res1 = await axios.get("https://gorana.onrender.com/products");
        this.products = res1.data.results.map((product) => {
            product.images[0] = product.images[0].replace("http", "https");
            return product;
        });
        this.set_products(this.products);
    },
    computed: {
        featuredProducts() {
            return this.products.slice(1, 5);
        },
        newArrivals() {
            return this.products.slice(5, 9);
        },
    },
    methods: {
        ...mapActions(["set_products"]),
    },
    components: {
        ServiceSection,
        BannerSection,
        NewArrivals,
        AdvertSection,
        FeaturedProducts,
        ActionButton,
        MainHeader,
        NewsLetter,
        MainFooter,
    },
};
</script>

<style scoped>
/* Hero Section */
.hero__section {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    height: calc(100vh - 65px);
    overflow: hidden;
    padding-block: 10px;
}

.hero__image {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    z-index: -1;
}

.hero__text {
    position: relative;
    color: white;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.6);
    z-index: 1;
}
.container {
    z-index: 1;
    position: relative;
}

.hero__text h4 {
    padding-bottom: 1rem;
}

/* .hero__text h1 {
    color: var(--dim-blue);
} */

.hero__text p {
    margin-bottom: 1rem;
    /* text-shadow: none; */
    font-weight: bold;
}
@media (max-width: 799px) {
    .hero__section {
        height: auto; 
    }

}

@media (min-width: 2000px) {
    .hero__section {
        background-position: 70% 12%;
        background-size: contain;
        background-repeat: no-repeat;
        background-color: #e3e6f3;
        height: 50vh;
    }
}

@media (min-width: 3000px) {
    .hero__section {
        background-position: 60% 30%;
    }
}
</style>
