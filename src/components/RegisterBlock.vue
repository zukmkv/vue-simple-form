<template>
    <div class="register-block">
        <h3 class="regblock-header"> {{ header }} </h3>
        <slot></slot>
    </div>
</template>

<script>

export default {
    name: 'register-block',
    props: ['header'],
}
</script>

<style lang="scss">
    @import "../styles/general";

    .regblock-header {
        padding: 0 1rem;
        margin: 0;
        @include ff(Roboto, 1.4rem);
    }
</style>