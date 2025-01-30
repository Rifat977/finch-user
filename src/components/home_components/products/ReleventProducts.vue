<template>
    <section class="products">
        <h2>Relevant Products</h2>
        <p class="highlight">Explore related you may love.</p>

        <!-- Swiper for Mobile -->
        <swiper
            v-if="isMobile"
            :slides-per-view="2"
            :space-between="15"
            :loop="true"
            :pagination="{ clickable: true }"
            class="product__slider"
        >
            <swiper-slide
                v-for="(product, index) in featuredProducts"
                :key="index"
                class="swiper__slide"
            >
                <product-card
                    :productId="product._id"
                    :productName="product.name"
                    :brand="product.brand"
                    :price="product.price"
                    :currency="product.currency"
                    :ratings="product.rating"
                    :image_url="product.images[0]"
                    :in_stock="product.in_stock"
                />
            </swiper-slide>
        </swiper>

        <!-- Grid Layout for Larger Screens -->
        <div class="product__container" v-else>
            <product-card
                v-for="(product, index) in featuredProducts"
                :key="index"
                :productId="product._id"
                :productName="product.name"
                :brand="product.brand"
                :price="product.price"
                :currency="product.currency"
                :ratings="product.rating"
                :image_url="product.images[0]"
                :in_stock="product.in_stock"
            />
        </div>

        <product-preloader type="inline" v-if="!featuredProducts">
            Loading products...
        </product-preloader>
    </section>
</template>

<script>
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import "swiper/css/pagination";
import ProductCard from "@/components/home_components/cards/ProductCard.vue";
import ProductPreloader from "@/components/preloaders/ProductPreloader.vue";

export default {
    name: "RelevantProducts",
    components: {
        ProductCard,
        ProductPreloader,
        Swiper,
        SwiperSlide,
    },
    props: ["featuredProducts"],
    data() {
        return {
            isMobile: window.innerWidth <= 768,
        };
    },
    mounted() {
        window.addEventListener("resize", this.checkMobile);
    },
    beforeUnmount() {
        window.removeEventListener("resize", this.checkMobile);
    },
    methods: {
        checkMobile() {
            this.isMobile = window.innerWidth <= 768;
        },
    },
};
</script>

<style scoped>
.products {
    text-align: center;
    margin-block: 4rem;
}

.products h2 {
    display: inline-block;
    margin-bottom: 10px;
}

.products .highlight {
    font-size: 1.6rem;
    margin-bottom: 20px;
}

/* Grid Layout for Desktop */
.product__container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 25px;
    padding: 3rem 1rem;
}

/* Swiper Styles */

.swiper__slide {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100% !important;  /* Force Swiper slides to be within the correct width */
    flex: 0 0 auto; /* Prevent shrinking/overlapping */
    box-sizing: border-box;
}

/* Fix Swiper Slide Issues */
.swiper-slide > * {
    width: 100%;
    height: 100%;
}

/* Responsive Design */
@media (max-width: 768px) {
    .product__container {
        display: none;
    }
}

@media (max-width: 480px) {
    .products {
        margin-block: 1rem;
    }

    .products h2 {
        font-size: 3rem;
    }

    .products .highlight {
        font-size: 1.9rem;
    }
}
</style>
