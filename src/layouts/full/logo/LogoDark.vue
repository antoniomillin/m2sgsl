<script setup lang="ts">
import { RouterLink } from 'vue-router';
import logo from '@/assets/images/logos/logo.svg';
</script>
<template>
    <div class="logo px-10">
        <RouterLink to="/">
            <img :src="logo" alt="home" />
        </RouterLink>
    </div>
</template>
