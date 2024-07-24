<template>
    <section class="section-swiper">
        <SectionSwiper></SectionSwiper>
    </section>
    <section class="section-contact">
        <SectionContact></SectionContact>
    </section>
    <section class="section-movies">
        <SectionMovies></SectionMovies>
    </section>
</template>
<script>
import SectionContact from '@/components/sections/SectionContact.vue';
import SectionMovies from '@/components/sections/SectionMovies.vue';
import SectionSwiper from '@/components/sections/SectionSwiper.vue';
export default {
    name: "MainPage",
    components: {
        SectionContact,
        SectionMovies,
        SectionSwiper
    }
}
</script>
<style>
    .section-contact {
        margin-top: 60px;
    }
    .section-movies {
        margin-top: 100px;
    }
</style>