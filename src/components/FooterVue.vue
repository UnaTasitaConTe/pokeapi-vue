<template>
    <footer class="d-flex flex-wrap justify-content-between text-center align-items-center py-3  border-top">
        <p class="col-md-4 mb-0 text-muted text-center"><b>&copy; 2023 TASITCONTE</b></p>
        <ul class=" nav col-md-4 justify-content-end">
            <li class="nav-item"><a href="https://github.com/Tasitaconte" target="_blank"
                    class="nav-link px-2 text-muted"><span>
                        {{ nombre.toUpperCase() }}
                    </span></a>
            </li>

        </ul>
    </footer>
</template>

<style>
footer {
    background-color: aliceblue;
    padding: 200px;
    bottom: 0;
}
</style>

<script>
export default {

    data() {
        return {
            nombre: 'github'
        }
    }
}
</script>