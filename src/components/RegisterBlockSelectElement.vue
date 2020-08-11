<template>
    <div class="select-el">
        <label class="select-el__label" :for="title">
            <slot></slot>
        </label>
        <select @click="check" class="select-el__field" :name=title v-model=value>
            <option v-for="item in data">
                {{ item }}
            </option>
        </select>
        <div v-if="($v.value.$dirty && !$v.value.required)" class="error">{{error}}</div>
        <div v-else class="error"></div>
    </div>
</template>

<script>
import { validationMixin } from 'vuelidate';
import { required } from 'vuelidate/lib/validators';
export default {
    mixins: [validationMixin],
    name: 'register-block-select-element',
    props: {
        title: String,
        data: Array,
        error: String,
    },
    data() {
        return {
            key: this.title,
            value: '',
        }
    },
    watch: {
        value: function () {
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
        }
    }
}
</script>

<style lang="scss">
    @import "../styles/general";

    .select-el {
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