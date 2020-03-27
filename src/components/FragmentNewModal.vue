<template>
    <v-dialog v-model="showingNew" persistent max-width="600px">
        <v-card>
            <v-card-title>
                <span class="headline">New movie</span>
            </v-card-title>
            <v-card-text>
                <v-container>
                    <v-row>
                        <v-col>
                            <v-text-field label="Title*" required outlined v-model="title" counter="15">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-textarea label="Description*" required outlined v-model="plot">
                            </v-textarea>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Genre*" required outlined v-model="genre">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Language*" required outlined v-model="language">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-label>Release Date*</v-label>
                            <v-date-picker v-model="date" full-width>
                            </v-date-picker>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Poster URL*" outlined v-model="poster">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-row>
                                <v-col cols="4">
                                    <v-text-field label="Producer Name*" v-model="name">
                                    </v-text-field>
                                </v-col>
                                <v-col cols="4">
                                    <v-text-field label="Producer nationality*" v-model="country">
                                    </v-text-field>
                                </v-col>
                                <v-col cols="4">
                                    <v-text-field label="Producer birth date*" v-model="birth">
                                    </v-text-field>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>
                </v-container>
                <small>*indicates required field</small>
            </v-card-text>
            <v-card-actions>
                <v-spacer>
                </v-spacer>
                <v-btn color="blue darken-1" text @click="close">Close</v-btn>
                <v-btn color="blue darken-1" text @click="save">Save</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    export default {
        name: "FragmentNewModal",
        props: {
            showingNew: Boolean
        },
        data: function () {
            return {
                title: '',
                date: '',
                poster: '',
                plot: '',
                name: '',
                country: '',
                birth: '',
                genre: '',
                language: '',
            }
        },
        methods: {
            save() {
                this.$emit('created', {
                    title: this.title,
                    date: this.date,
                    plot: this.plot,
                    poster: this.poster,
                    name: this.name,
                    country: this.country,
                    birth: this.birth,
                    genre: this.genre,
                    language: this.language,
                });
                this.title = '';
                this.language = '';
                this.genre = '';
                this.poster = '';
                this.plot = '';
                this.date = '';
                this.country = '';
                this.birth = '';
                this.name = '';
            },
            close() {
                this.$emit('closed');
            }
        }
    }
</script>

<style scoped>

</style>