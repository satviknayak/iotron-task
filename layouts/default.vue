<template>
    <div class="flex w-full min-h-[200vh] bg-slate-900 flex-col text-white">
        <Header />
        <slot />
    </div>
</template>

<script setup>
    import Header from '~/components/Header.vue';
</script>
