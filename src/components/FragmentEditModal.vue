<template>
    <v-dialog v-model="showing" persistent max-width="600px">
        <v-card>
            <v-card-title>
                <span class="headline">Modifier le film {{ title }}</span>
            </v-card-title>
            <v-card-text>
                <v-container>
                    <v-row>
                        <v-col>
                            <v-text-field label="Title*" required outlined v-model="editedProps.title" counter="15">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-textarea label="Description*" required outlined v-model="editedProps.plot">
                            </v-textarea>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Genre*" required outlined v-model="editedProps.genre">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Language*" required outlined v-model="editedProps.language">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-label>Release Date*</v-label>
                            <v-date-picker v-model="editedProps.date" full-width>
                            </v-date-picker>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field label="Poster URL*" outlined v-model="editedProps.poster">
                            </v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-row>
                                <v-col cols="4">
                                    <v-text-field label="Producer Name*" v-model="editedProps.name">
                                    </v-text-field>
                                </v-col>
                                <v-col cols="4">
                                    <v-text-field label="Producer nationality*" v-model="editedProps.country">
                                    </v-text-field>
                                </v-col>
                                <v-col cols="4">
                                    <v-text-field label="Producer birth date*" v-model="editedProps.birth">
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
        name: "FragmentEditModal",
        props: {
            showing: Boolean,
            title: String,
            date: String,
            plot: String,
            poster: String,
            name: String,
            country: String,
            birth: String,
            genre: String,
            language: String,
        },
        data: function () {
            return {
                editedProps: {
                    title: this.title,
                    date: this.date,
                    plot: this.plot,
                    poster: this.poster,
                    birth: this.birth,
                    country: this.country,
                    name: this.name,
                    genre: this.genre,
                    language: this.language,
                },
            }
        },
        methods: {
            close() {
                this.$emit('closed');
            },
            save() {
                let newMovie = {
                    title: this.editedProps.title,
                    date: this.editedProps.date,
                    plot: this.editedProps.plot,
                    poster: this.editedProps.poster,
                    birth: this.editedProps.birth,
                    country: this.editedProps.country,
                    name: this.editedProps.name,
                    language: this.editedProps.language,
                    genre: this.editedProps.genre,
                };
                this.$emit('saved', newMovie);
            }
        }
    }
</script>

<style scoped>

</style>