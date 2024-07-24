<template>
    <div class="swiper-wrapper">
        <swiper
            :grabCursor="false"
            :loop="true"
            :effect="'creative'"
            :allowTouchMove="false"
            :speed="1000"
            :navigation="{
                nextEl: '.next-arrow'
            }"
            :creativeEffect="{
                prev: {
                    translate: ['-30%', 0, -200],
                    opacity: 1,
                },
                next: {
                    translate: ['100%', 0, 0],
                    opacity: 0,
                },
                shadowPerProgress: true
            }"
            :modules="modules"
            class="mySwiper"
        >
            <swiper-slide v-for="(color, index) in slideColors" :key="index">
                <swiper-card :color="color" :slideIndex="index+1" :slidesCount="slideColors.length"></swiper-card>
            </swiper-slide>
        </swiper>
        <img class="next-arrow" src="../../assets/images/arrowNext.svg" alt="">
    </div>
</template>
<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import 'swiper/css';
import 'swiper/css/effect-cards';
import { ref } from 'vue';
import { EffectCreative, Navigation } from 'swiper/modules';
import SwiperCard from '@/components/elements/SwiperCard.vue';
export default {
    name: "SectionSwiper",
    components: {
      Swiper,
      SwiperSlide,
      SwiperCard
    },
    setup() {
        const mySwiper = ref(null)
        const slideColors = ['#027D84', '#C70039', '#61FF33']
        return {
            modules: [EffectCreative, Navigation],
            mySwiper,
            slideColors
        };
    },
}
</script>
<style>
    .button-next {
        display: flex;
        justify-content: center;
        align-items: center;
        padding: 10px 25px;
        border: 1px solid black;
    }
    .next-arrow {
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        right: 80px;
        z-index: 2;
    }
    @media screen and (max-width: 768px) {
        .next-arrow {
            right: 35px;
        }
    }
    @media screen and (max-width: 576px) {
        .next-arrow {
            width: 90px;
            height: 90px;
        }
    }
</style>