<template>
    <div class="swiper-card-wrapper" :style="{backgroundColor: color}">
        <div class="swiper-card-ellipse">
            <p class="swiper-header-text">Lorem ipsum dolor sit amet</p>
        </div>
        <img class="snow" src="../../assets/images/snow.svg" alt="">
        <div class="swiper-card-container">
            <div class="swiper-main-content">
                <div class="swiper-main-text">  
                    <span class="main-text-element">Lorem ipsum</span>
                    <span class="main-text-element">Lorem ipsum dolor — </span>
                    <span class="main-text-element">Lorem</span>
                    <span class="main-text-element">ipsum !</span>
                    <span class="main-text-element">Lorem ipsum dolor sit amet, consectetur adipiscing elit</span>
                </div>
                <div class="swiper-main-image">
                    <img src="../../assets/images/image.png" alt="">
                </div>
            </div>
        </div>
        <span class="count-slides">{{ slideIndex }}/{{ slidesCount }}</span>
    </div>
</template>
<script>
export default {
    name: 'SwiperCard',
    props: {
        color: String,
        slideIndex: Number,
        slidesCount: Number
    }
}
</script>
<style>
    .swiper-card-wrapper {
        padding: 0 25px 50px;
        text-transform: uppercase;
        position: relative;
    }
    .snow {
        position: absolute;
        bottom: 15%;
    }
    .elipse {
        position: absolute;
        top: 0;
        z-index: 2;
        left: 200px;
    }
    .count-slides {
        padding: 15px 40px;
        border-radius: 100%;
        border: 2px solid white;
        color: white;
        position: absolute;
        left: 300px;
        bottom: 50px;
    }
    .next-arrow:hover {
        cursor: pointer;
    }
    .swiper-card-container {
        max-width: 1350px;
        margin: 0 auto;
        color: white;
    }
    .swiper-header-text {
        position: relative;
        margin-left: 50px;
        font-size: 18px;
        text-shadow: 4px 4px 4px rgba(0, 0, 0, 0.25);
        z-index: 3;
    }
    .swiper-main-content {
        display: flex;
    }
    .swiper-main-text {
        margin-top: 75px;
        display: flex;
        flex-direction: column;
        gap: 15px;
    }
    .swiper-main-image img {
        width: 100%;
        height: 100%;
        max-width: 550px;
        max-height: 550px;
        margin-top: 50px;
    }
    .main-text-element {
        font-size: 60px;
        white-space: nowrap;
    }
    .main-text-element:first-child {
        font-weight: bold;
    }
    .main-text-element:nth-child(2) {
        margin-left: 40px;
    }
    .main-text-element:nth-child(3) {
        margin-left: 290px;
    }
    .main-text-element:nth-child(4) {
        margin-left: 140px;
    }
    .main-text-element:last-child {
        font-size: 15px;
        max-width: 278px;
        line-height: 1.5;
        margin-top: 30px;
        margin-left: 290px;
        white-space: wrap;
    }

    .swiper-card-ellipse {
        width: 450px;
        height: 77px;
        position: relative;
        background-image: url('@/assets/images/elipse.svg');
        background-repeat: no-repeat;
        background-size: contain;
        color: white;
    }

    .swiper-header-text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        white-space: nowrap;
    }
    @media screen and (max-width: 1200px) {
        .swiper-card-wrapper {
            margin: 0 auto;
        }
        .swiper-main-content {
            flex-direction: column;
            align-items: center;
        }
        .swiper-main-image img {
            max-width: 450px;
            max-height: 450px;
        }
        .snow {
            bottom: 45%;
        }
        .count-slides {
            left: 50px;
        }
    }
    @media screen and (max-width: 768px) {
        .main-text-element {
            font-size: 40px;
        }
        .main-text-element:nth-child(3) {
            margin-left: 240px;
        }
        .main-text-element:nth-child(4) {
            margin-left: 120px;
        }
        .main-text-element:last-child {
            margin-top: 0;
        }
        .next-arrow {
            right: 35px;
        }
        .count-slides {
            left: 20px;
        }
    }
    @media screen and (max-width: 576px) {
        .swiper-card-ellipse {
            width: 100%;
            background-size: 100% 100%;
        }
        .main-text-element {
            font-size: 30px;
        }
        .snow {
            display: none;
        }
        .swiper-main-image img {
            max-width: 350px;
            max-height: 350px;
        }
        .swiper-main-content {
            align-items: center;
        }
        .next-arrow {
            width: 90px;
            height: 90px;
        }
        .main-text-element:last-child {
            margin-left: 0;
            font-size: 12px;
        }
        .count-slides {
            bottom: 20px;
        }
    }
</style>