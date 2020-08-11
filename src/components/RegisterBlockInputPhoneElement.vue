<template>
    <div class="input-tel-el">
        <label class="input-tel-el__label" :for="title">
            <slot></slot>
        </label>
        <input @input="check" class="input-tel-el__field" type="tel" :placeholder="placeholder" :name=title v-model="value">
        <div v-if="($v.value.$dirty && (!$v.value.between || !$v.value.required))" class="error">{{error}}</div>
        <div v-else class="error"></div>
    </div>
</template>

<script>
import { validationMixin } from 'vuelidate';
import { required, between } from 'vuelidate/lib/validators';
export default {
    mixins: [validationMixin],
    name: 'register-block-input-phone-element',
    props: ['title', 'placeholder', 'error'],
    data() {
        return {
            key: this.title,
            value: '',
        }
    },
    watch: {
        value: function (){
            this.$set(this.$parent.$parent._data, this.key, {value: this.value});
        }
    },
    methods: {
        check(){
            this.$v.$touch();
        }
    },
    validations: {
        value: {
            required,
            between: between(70000000000, 79999999999),
        }
    }
}
</script>

<style lang="scss">
    @import "../styles/general";

    .input-tel-el {
        display: flex;
        flex-direction: column;
        width: 100%;
        padding-right: 1rem;
        padding-left: 1rem;
        color: $clr-text;
        margin-bottom: 1rem;
        @include ff('Roboto', 1rem);

        &__field {
            background-color: $clr-input;
            width: 100%;
            height: 38px;
            padding: .375rem .75rem;
            border: 1px solid darken($color: $clr-input, $amount: 10%);
            border-radius: .25rem;
            @include ff('Roboto', 1rem);
        }

        &__label {
            margin-bottom: 0.5rem;
        }
    }
</style>