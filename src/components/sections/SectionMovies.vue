<template>
    <div class="movies-container">
        <div class="movie-controllers">
            <div class="movies-controller-element">
                <input class="controller-input" type="checkbox" v-model="controllers.sortByAlph" @change="makeSortByAlph">
                <p class="controller-text">Відсортувати блоки за алфавітом</p>
            </div>
            <div class="movies-controller-element">
                <input class="controller-input" type="radio" v-model="controllers.sortByChessOrder" value="false">
                <p class="controller-text">Вивести блоки в форматі 'Зображення - текст'</p>
            </div>
            <div class="movies-controller-element">
                <input class="controller-input" type="radio" v-model="controllers.sortByChessOrder" value="true">
                <p class="controller-text">Вивести блоки в шаховому порядку</p>
            </div>
        </div>
        <div class="movies-wrapper">
            <MovieItem v-for="(movie, index) in sortedMovies" :key="index" :movie="movie" :chess-order="JSON.parse(controllers.sortByChessOrder)" :index="index+1"></MovieItem>
        </div>
    </div>
</template>
<script>
import { ref, onMounted } from 'vue';
import MovieItem from '@/components/elements/Movie.vue';
export default {
    name: "SectionMovies",
    components: {
        MovieItem
    },
    setup() {
        const movies = ref([])
        const sortedMovies = ref([])
        const controllers = ref({
            sortByAlph: false,
            sortByChessOrder: 'false'
        })
        const getMovies = async() => {
            try {
                const response = await fetch('https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1')
                const data = await response.json()
                console.log(await data.results.slice(0, 5))
                movies.value = data.results.slice(0, 5)
                sortedMovies.value = data.results.slice(0, 5)
            } catch(e) {
                console.log(e)
            }
        }
        const makeSortByAlph = () => {
            console.log(controllers.value.sortByAlph)
            if (controllers.value.sortByAlph) {
                sortedMovies.value.sort((a, b) => (new Intl.Collator('en')).compare(a.title, b.title))
            } else {
                console.log('back')
                sortedMovies.value = [...movies.value]
                console.log(movies.value)
            }
        }
        onMounted(() => {
            getMovies()
        })
        return {
            movies,
            sortedMovies,
            controllers,
            makeSortByAlph
        }
    }
}
</script>
<style>
    .movies-container {
        max-width: 1020px;
        margin: 0 auto;
    }
    .movies-wrapper {
        display: flex;
        flex-direction: column;
        gap: 40px;
        margin-top: 50px;
    }
    .movie-controllers {
        display: flex;
        flex-direction: column;
        gap: 10px;
    }
    .movies-controller-element {
        display: flex;
        align-items: center;
        gap: 5px;
    }
    .controller-text {
        margin-top: 5px;
    }
    .controller-input {
        border-radius: 100%;
    }
</style>