<script setup lang="ts">
import { RouterLink } from 'vue-router';
import Darklogo from '@/assets/images/logos/logo.svg';
</script>
<template>
    <div class="logo px-10">
        <RouterLink to="/">
            <img :src="Darklogo" alt="home" />
        </RouterLink>
    </div>
</template>
