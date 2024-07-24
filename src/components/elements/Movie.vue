<template>
    <div class="movie-element">
        <div class="movie-image" :class="{'chess-order-image': chessOrder && index % 2 == 0}" :style="{backgroundImage: `url(https://image.tmdb.org/t/p/w185_and_h278_bestv2/${movie.poster_path})`}"></div>
        <div class="movie-text" :class="{'chess-order-text': chessOrder && index % 2 == 0}">
            <h3 class="movie-title">{{ movie.title }}</h3>
            <p class="movie-overview">{{ movie.overview }}</p>
        </div>
    </div>
</template>
<script>
export default {
    name: "MovieItem",
    props: {
        movie: Object,
        chessOrder: Boolean,
        index: Number
    }
}
</script>
<style>
    .movie-element {
        background-color: #C4C4C4;
        padding: 30px 50px 30px 35px;
        display: flex;
        gap: 50px;
        align-items: center;
    }
    .movie-image {
        width: 380px;
        height: 260px;
        background-color: white;
        flex-shrink: 0;
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
    }
    .movie-text {
        display: flex;
        flex-direction: column;
        gap: 30px;
    }
    .movie-text h3 {
        font-size: 25px;
    }
    .chess-order-image {
        order: 2;
    }
    .chess-order-text {
        order: 1;
    }
    @media screen and (max-width: 768px) {
        .movie-element {
            flex-direction: column;
            justify-content: center;
            margin: 0 auto;
            text-align: center;
            padding: 30px 35px 30px 35px;
        }
        .movie-image {
            width: 300px;
            height: 260px;
        }
    }
</style>