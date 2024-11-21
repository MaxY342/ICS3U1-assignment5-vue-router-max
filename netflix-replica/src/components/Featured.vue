<script>

</script>

<template>
    <div class="featured-section">
        <h1>Featured</h1>
        <div class="featured-section-content">
            <img src="../assets/grey.webp" alt="movie" width="250" height="350">
            <img src="../assets/grey.webp" alt="movie" width="250" height="350">
            <img src="../assets/grey.webp" alt="movie" width="250" height="350">
        </div>
    </div>
</template>

<style scoped>
    .featured-section {
        text-align: center;
    }

    .featured-section {
        z-index: 2;
        background-color: #151515;
        color: white;
        position: relative;
        font-size: 20px;
        padding: 40px 100px;
    }

    .featured-section-content {
        display: grid;
        grid-template-columns: auto auto auto;
        justify-items: center;
    }
</style>

