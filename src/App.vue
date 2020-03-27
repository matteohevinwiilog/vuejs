<template>
    <v-app>
        <ListRecycler>
        </ListRecycler>
    </v-app>
</template>

<script>
    import ListRecycler from './components/ListRecycler';

    export default {
        name: 'App',

        components: {
            ListRecycler,
        },

        data: () => ({
            //
        }),
    };
</script>
