<script setup>

</script>

<template>
    <div class="topbar">
            <div class="sidebar">
                <button class = sidebarbtn>Menu</button>
                <div class="sidebar-content">
                    <RouterLink to="/">Homepage</RouterLink>
                    <a>Subscription Plans</a>
                    <a>Trending</a>
                    <a>Most Popular</a>
                    <a>New</a>
                </div>
            </div>
            <h1 class="logo">Metflix</h1>
            <RouterLink to="/signup" class="sign-up-btn">Sign-up</RouterLink>
            <RouterLink to="/login" class="log-in-btn">Login</RouterLink>
        </div>
</template>

<style scoped>
    .topbar {
        display: grid;
        grid-template-columns: auto auto 1fr auto auto;
        gap: 10px;
        margin-top: 10px;
        margin-bottom: 10px;
        align-items: center;
    }

    .sign-up-btn {
        grid-column: 4/4;
    }

    .sidebarbtn, .sign-up-btn, .log-in-btn {
        background-color: #191919;
        color: white;
        padding: 10px;
        font-size: 16px;
        border: none;
        z-index: 1;
        text-decoration: none;
    }

    .sidebar-content {
        display: none;
        position: fixed;
        background-color: #444444;
        width: 300px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        z-index: 3;
        top: 0;
        height: 100vh;
        overflow: hidden;
        white-space: nowrap;
    }

    .sidebar-content a {
        color: white;
        padding: 18px 16px;
        text-decoration: none;
    }

    .sidebar:hover .sidebar-content {
        display: grid;
        animation-name: slide;
        animation-duration: 1s;
        grid-template-rows: auto auto auto auto auto 1fr;
    }

    @keyframes slide {
        from {width: 0px;}
        to {width: 300px;}
    }

    .sidebarbtn:hover, .sign-up-btn:hover, .log-in-btn:hover {
        background-color: #353535
    }

    .sidebar-content a:hover {
        background-color: #4f4f4f;
    }

    .topbar:hover ~ * {
        opacity: 0.5;
    }

    .logo {
        margin: 0;
        grid-column: 2/2;
        color: red;
        margin-left: 20px;
    }
</style>