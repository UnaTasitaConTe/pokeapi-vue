<template>

    <div>
        <!-- {{ hola }} -->
        {{ pokemon_info }}

    </div>

</template>

<script>
export default {
    props: {
        pokemon_info: []
    },
    data() {
        return {
            // hola: 'hola amigos'
        }
    }
}
</script>