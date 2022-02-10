<template>
    <div class="app-container">
        <Header>Vuejs todos</Header>

        <slot />
    </div>
</template>

<script>
import Header from './Header.vue';
export default {
    components:{
        Header,
    }
}
</script>