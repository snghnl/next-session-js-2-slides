<template>
    <footer
        class="absolute bottom-4 left-0 right-0 flex justify-between items-center px-8 text-xs text-gray-400"
    >
        <img src="./assets/next-logo.png" class="h-2" />
        <span>{{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}</span>
    </footer>
</template>
