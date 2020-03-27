<template>
    <v-container>
        <v-container v-if="!$route.params.id">
            <FragmentNewModal :showing-new="showingNew"
                              @closed="handleClose"
                              @created="handleCreation">
            </FragmentNewModal>
            <v-row>
                <v-col cols="9">
                    <v-text-field label="Search..."
                                  v-model="search"
                                  @input="searchChanged">
                    </v-text-field>
                </v-col>
                <v-col cols="3" class="pt-6">
                    <v-btn @click="showingNew = true">
                        New movie
                    </v-btn>
                </v-col>
            </v-row>
            <v-row>
                <v-col v-for="movie in moviesFiltered"
                       cols="3"
                       :key="movie.id">
                    <ListFragment
                            :title="movie.title"
                            :date="movie.date"
                            :plot="movie.plot"
                            :poster="movie.poster"
                            :country="movie.country"
                            :name="movie.name"
                            :birth="movie.birth"
                            :genre="movie.genre"
                            :language="movie.language"
                            :rating="movie.rating"
                            @deleted="handleDelete"
                            @modified="handleModification"
                            :id="movie.id">
                    </ListFragment>
                </v-col>
            </v-row>
        </v-container>
        <router-view v-if="$route.params.id">
        </router-view>
    </v-container>
</template>

<script>
    import ListFragment from "@/components/ListFragment";
    import Vue from 'vue'
    import FragmentNewModal from "@/components/FragmentNewModal";
    import VueRouter from "vue-router";

    Vue.use(VueRouter);
    export default {
        name: "ListRecycler",
        data: function () {
            return {
                movies: [],
                moviesFiltered: [],
                search: '',
                showingNew: false
            }
        },
        components: {
            FragmentNewModal,
            ListFragment
        },
        watch: {
            $route() {
                this.searchChanged();
            }
        },
        methods: {
            searchChanged() {
                this.moviesFiltered = this.movies.filter((movie) => {
                    return movie.title.toLowerCase().includes(this.search.toLowerCase())
                        || movie.date.toLowerCase().includes(this.search.toLowerCase())
                        || movie.plot.toLowerCase().includes(this.search.toLowerCase())
                        || movie.name.toLowerCase().includes(this.search.toLowerCase())
                        || movie.genre.toLowerCase().includes(this.search.toLowerCase())
                        || movie.country.toLowerCase().includes(this.search.toLowerCase())
                });
            },
            handleModification(newMovie) {
                let movieToEdit = this.movies.find(movie => movie.id === newMovie.id);
                Vue.set(this.movies, this.movies.indexOf(movieToEdit), {
                    ...movieToEdit,
                    ...newMovie
                });
                this.searchChanged();
            },
            handleDelete(id) {
                let movieFilteredToDeleteIndex = this.moviesFiltered.findIndex(movie => movie.id === id);
                let movieToDeleteIndex = this.movies.findIndex(movie => movie.id === id);
                this.movies.splice(movieToDeleteIndex, 1);
                this.moviesFiltered.splice(movieFilteredToDeleteIndex, 1);
                this.searchChanged();
            },
            handleCreation(newMovie) {
                let newMovieWithId = {
                    ...newMovie,
                    id: new Date().valueOf().toString()
                };
                this.movies.push(newMovieWithId);
                this.moviesFiltered.push(newMovieWithId);
                this.searchChanged();
                this.showingNew = false;
            },
            handleClose() {
                this.showingNew = false;
            }
        }
    }
</script>

<style scoped>
</style>