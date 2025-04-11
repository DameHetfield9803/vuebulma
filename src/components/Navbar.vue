<script setup>
import { ref, computed, onMounted } from 'vue'
import About from './About.vue'
import Home from './Home.vue'
import NotFound from './NotFound.vue'
import Themeswitch from './Themeswitch.vue'
const routes = {
    '/': Home,
    '/about': About,
}
const currentPath = ref(window.location.hash)
window.addEventListener('hashchange', () => {
    currentPath.value = window.location.hash
})
const currentView = computed(() => {
    return routes[currentPath.value.slice(1) || '/'] || NotFound
})

// hamburger time

onMounted(() => {

    // Get all "navbar-burger" elements
    const $navbarBurgers = Array.prototype.slice.call(document.querySelectorAll('.navbar-burger'), 0);

    // Add a click event on each of them
    $navbarBurgers.forEach(el => {
        el.addEventListener('click', () => {

            // Get the target from the "data-target" attribute
            const target = el.dataset.target;
            const $target = document.getElementById(target);

            // Toggle the "is-active" class on both the "navbar-burger" and the "navbar-menu"
            el.classList.toggle('is-active');
            $target.classList.toggle('is-active');
        });
    });

});
</script>
<template>
    <nav class="navbar buttons p-1" role="navigation">
        <div class="navbar-start">
            <div class="navbar-brand button">
                <a href="/" class="navbar-item">Home</a>
            </div>
        </div>
        <div class="navbar-menu">
            <a href="#/about" class="navbar-item">About</a>
            <a href="#/non-existent-path" class="navbar-item">Broken Link</a>
            <a class="navbar-item">
                <Themeswitch />
            </a>
        </div>
        <div class="navbar-end">
            <a role="button" class="navbar-burger is-hidden-desktop" aria-label="menu" aria-expanded="true" data-target="navbarMenuHero">
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
                <span aria-hidden="true"></span>
            </a>
        </div>
        <div id="navbarMenuHero" class="navbar-menu pb-1 is-hidden-desktop">
            <div class="navbar-end">
                <ul class="py-2">
                    <li class="py-1"><a class="navbar-item button is-rounded" href="#/about">About</a></li>
                    <li><a class="navbar-item button is-rounded" href="#/non-existent-path">Broken Link</a></li>
                </ul>
            </div>
        </div>
    </nav>
    <hr />
    <component :is="currentView" class="has-text-centered container is-widescreen " />
</template>
