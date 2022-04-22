<template>

    <div id="contenitore" class="h-100 px-3">
        <!-- Titolo -->
        <h1>Boolzap</h1>

        <!-- Input e button per ricerca film -->
        <div class="input-group">

            <!-- Input -->
            <input type="text" class="form-control" placeholder="Search a movie" aria-label="Recipient's username"
                aria-describedby="button-addon2" v-model="searchText" v-on:keyup.enter="$emit('sendText', searchText)">

            <!-- Button -->
            <button class="btn btn-outline-danger" type="button" id="button-addon2"
                @click.enter="$emit('sendText', searchText)">
                Button
            </button>

        </div>

    </div>

</template>

<script>
    export default {
        name: 'HeaderComp',

        data() {
            return {

                searchText: null

            }
        }
    }
</script>

<style lang="scss" scoped>

    @import "../assets/style/variabili.scss";
    @import "../assets/style/mixin.scss";

    #contenitore {
        @include flex(row, space-between, center);

        h1 {
            color: $color-title;
            // Annullo il margin button di default
            margin-bottom: 0;
        }

        .input-group {
            width: 15%;

            button {
                color: $color-title;
                border-color: $color-title;
            }

            .btn-outline-danger:hover {
                background-color: red;
                color: black;
            }
        }

    }
</style>