<template>
    <div class="movie">
        <FragmentEditModal :showing="showingEdit"
                           :title="editedProps.title"
                           :date="editedProps.date"
                           :plot="editedProps.plot"
                           :poster="editedProps.poster"
                           :country="editedProps.country"
                           :name="editedProps.name"
                           :birth="editedProps.birth"
                           :genre="editedProps.genre"
                           :language="editedProps.language"
                           @saved="handleSaved"
                           @closed="handleCloseEdit">
        </FragmentEditModal>
        <FragmentDeleteModal :showing="showingDelete"
                             :id="id"
                             @canceled="showingDelete = false"
                             @confirmed="handleDelete">
        </FragmentDeleteModal>
        <v-card class="movie-card">
            <v-img :src="editedProps.poster" class="card-image" @click="handleClicked">
            </v-img>
            <v-card-title class="card-title" @click="handleClicked">
                {{ editedProps.title }}
            </v-card-title>
            <v-card-text class="card-content" @click="handleClicked">
                {{ editedProps.plot }}
            </v-card-text>
            <v-card-actions class="card-actions">
                <v-spacer>
                </v-spacer>
                <v-btn icon>
                    <v-icon>mdi-star</v-icon>
                </v-btn>
                <v-btn icon>
                    <v-icon @click="showingEdit = true">mdi-pencil</v-icon>
                </v-btn>
                <v-btn icon>
                    <v-icon @click="showingDelete = true">mdi-delete</v-icon>
                </v-btn>
            </v-card-actions>
        </v-card>
    </div>
</template>

<script>
    import FragmentEditModal from "@/components/FragmentEditModal";
    import FragmentDeleteModal from "@/components/FragmentDeleteModal";

    export default {
        name: 'ListFragment',
        components: {FragmentDeleteModal, FragmentEditModal},
        data: function () {
            return {
                showingEdit: false,
                showingDelete: false,
                editedProps: {
                    title: this.title,
                    date: this.date,
                    plot: this.plot,
                    poster: this.poster !== "" ? this.poster : "https://www.labaleine.fr/sites/baleine/files/image-not-found.jpg",
                    name: this.name,
                    country: this.country,
                    birth: this.birth,
                    genre: this.genre,
                    language: this.language,
                },
            }
        },
        props: {
            title: String,
            date: String,
            id: String,
            plot: String,
            poster: String,
            name: String,
            country: String,
            birth: String,
            genre: String,
            language: String,
        },
        methods: {
            handleCloseEdit() {
                this.showingEdit = false;
            },
            refreshCardAndList(newMovie) {
                this.editedProps.title = newMovie.title;
                this.editedProps.date = newMovie.date;
                this.editedProps.plot = newMovie.plot;
                this.editedProps.poster = newMovie.poster;
                this.editedProps.country = newMovie.country;
                this.editedProps.name = newMovie.name;
                this.editedProps.birth = newMovie.birth;
                this.editedProps.genre = newMovie.genre;
                this.editedProps.language = newMovie.language;
                this.$emit('modified', {
                    id: this.id,
                    ...newMovie
                });
            },
            handleSaved(newMovie) {
                this.handleCloseEdit();
                this.refreshCardAndList(newMovie);
            },
            handleDelete() {
                this.$emit('deleted', this.id);
            },
            handleClicked() {
                this.$router.push({
                    name: 'movieDetail',
                    params: {
                        id: this.id
                    },
                    query: {
                        movie: {
                            title: this.editedProps.title,
                            date: this.editedProps.date,
                            id: this.id,
                            plot: this.editedProps.plot,
                            poster: this.editedProps.poster,
                            name: this.editedProps.name,
                            country: this.editedProps.country,
                            birth: this.editedProps.birth,
                            genre: this.editedProps.genre,
                            language: this.editedProps.language,
                        }
                    }
                })
            }
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    .card-image {
        height: 40%;
    }

    .card-title {
        height: 10%;
    }

    .card-content {
        height: 40%;
    }

    .card-actions {
        height: 10%;
    }

    .movie {
        margin-bottom: 5px;
        height: 500px;
    }

    .movie-card {
        height: 100%;
        cursor: pointer;
    }

</style>
