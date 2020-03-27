<template>
    <div>
        <v-card>
            <v-card-title>
                <span class="headline">{{ selectedMovie.title }}</span>
                <v-spacer>
                </v-spacer>
                <v-btn color="blue darken-1" text @click="handleHome">Home</v-btn>
            </v-card-title>
            <v-card-text>
                <v-container>
                    <v-row>
                        <v-col>
                            <v-text-field label="Title" disabled outlined v-model="selectedMovie.title" counter="15">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-textarea label="Description" disabled outlined v-model="selectedMovie.plot">
                            </v-textarea>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Genre" disabled outlined v-model="selectedMovie.genre">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Language" disabled outlined v-model="selectedMovie.language">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-label>Release Date*</v-label>
                            <v-date-picker v-model="selectedMovie.date" full-width disabled>
                            </v-date-picker>
                        </v-col>
                        <v-col cols="12">
                            <v-img disabled :src="selectedMovie.poster">
                            </v-img>
                        </v-col>
                        <v-col cols="12">
                            <v-row>
                                <v-col cols="4">
                                    <v-text-field label="Producer Name" disabled v-model="selectedMovie.name">
                                    </v-text-field>
                                </v-col>
                                <v-col cols="4">
                                    <v-text-field label="Producer nationality" disabled v-model="selectedMovie.country">
                                    </v-text-field>
                                </v-col>
                                <v-col cols="4">
                                    <v-text-field label="Producer birth date" disabled v-model="selectedMovie.birth">
                                    </v-text-field>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>
                </v-container>
            </v-card-text>
            <v-card-actions>
                <v-spacer>
                </v-spacer>
                <v-btn color="blue darken-1" text @click="handleHome">Home</v-btn>
            </v-card-actions>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: "FragmentDetails",
        data: function() {
            return {
                selectedMovie: null
            }
        },
        created() {
            if (this.$route.query.movie) {
                this.selectedMovie = this.$route.query.movie;
            }
        },
        methods: {
            handleHome() {
                this.$router.go(-1);
            }
        }
    }
</script>

<style scoped>

</style>