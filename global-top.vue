<template>
    <footer class="absolute bottom-0 left-0 right-0 p-0 p-l-2 p-r-2 bg-sky-200 flex-container">
        <p class="text-s p-0 m-0">{{ $slidev.configs.title }}</p>
        <div class="flex-c2 p-0 p-l-2 p-r-2">
            <carbon:logo-github />
            <p class="text-s p-0 m-0">klef-project/lecture/{{ $slidev.configs.directory }}</p>
            <p class="text-s p-0 m-0 p-l-4"># {{ $slidev.nav.currentPage }}</p>
        </div>
    </footer>
</template>

<style>
    .flex-container{
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-between;
        align-items: center;
    }
    .flex-c2{
        display: flex;
        flex-wrap: nowrap;
        justify-content: end;
        align-items: center;
    }
</style>