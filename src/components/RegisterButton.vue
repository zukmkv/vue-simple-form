<template>
    <div class="wrap-btn">
        <button class="btn">
            <slot></slot>
        </button>
    </div>
</template>

<script>
export default {
    name: 'register-button',
}
</script>

<style lang="scss">
    @import "../styles/general";
    .wrap-btn {
        display: flex;
        justify-content: flex-end;
    }

    .btn {
        width: auto;
        height: auto;
        background-color: #59a9ff;
        @include ff('Roboto', 1.5rem);
        padding: .5rem;
        margin: 0 1rem 1rem 1rem;
        user-select: none;
        border-radius: .3rem;
        color: white;
        border: 1px solid transparent;
        cursor: pointer;
        transition: background-color .15s ease-in-out, opacity .15s ease-in-out;
        @media screen and (max-width: 510px){
            width: 100%;
        }

        &:hover {
            background-color: #bb8d54;
            opacity: .6;
        }
    }
</style>