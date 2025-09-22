<script setup lang="ts">
import { RouterLink } from 'vue-router';

</script>

<template>
<div>
<center>
<div class="utback">
    <img loading="lazy" class="duck" src="../assets/UtyaGold.gif">
</div>
    <h2>Create job search profiles<br>or look for a job</h2>
    <RouterLink style="text-decoration: none; color: black;" to="/home">
        <button class="next">Next</button>
    </RouterLink>
</center>
</div>
</template>

<style scoped>
h2 {
    font-family: Geologica;
    color: white;
}
</style>