<template>
    <v-dialog v-model="showing"
              persistent
              max-width="290">
        <v-card>
            <v-card-title class="headline">Delete movie ? </v-card-title>
            <v-card-text>
                Are you sure you want to delete this movie ?
            </v-card-text>
            <v-card-actions>
                <v-spacer>
                </v-spacer>
                <v-btn text
                       @click="cancel">
                    Cancel
                </v-btn>
                <v-btn text
                        @click="confirm">
                    Confirm
                </v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
    export default {
        name: "FragmentDeleteModal",
        props: {
            id: String,
            showing: Boolean,
        },
        methods: {
            confirm() {
                this.$emit('confirmed', this.id);
            },
            cancel() {
                this.$emit('canceled');
            }
        }
    }
</script>

<style scoped>

</style>