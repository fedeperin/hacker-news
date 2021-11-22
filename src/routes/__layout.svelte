<nav>
    <a href="./">👨‍💻</a>
</nav>

<div class="container">
    <slot></slot>
</div>

<style>
    nav {
        width: 100%;
        padding: 10px;
        background: #000;
        margin-bottom: 20px;
    }

    nav a {
        font-size: 40px;
    }

    .container {
        padding: 0 20px;
    }
</style>