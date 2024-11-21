<script setup>
    function ScrollOpacityEffect(item) {
        let header = document.querySelector(item);
        let scrollPosition = window.pageYOffset;
        header.style.opacity = 1 - scrollPosition / 400;
    };

    window.addEventListener('scroll', function() {
        ScrollOpacityEffect(".hero");
    });
</script>

<template>
    <div class="hero-container">
            <h1 class="hero">Watch Now!</h1>
    </div>
</template>

<style scoped>
    .hero-container {
        background-color: #2f2f2f;
        position: relative;
        padding: 18rem 1rem;
        display: flex;
        justify-content: center;
        align-items: center;
        transition: opacity 1s ease;
    }

    .hero {
        color: white;
        font-size: 10vh;
        position: fixed;
        text-align: center;
        z-index: 1;
    }
</style>
