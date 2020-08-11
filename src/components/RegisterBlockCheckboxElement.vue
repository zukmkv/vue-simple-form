<template>
    <div :name=title class="checkbox-el">
        <slot></slot>
        <ul>
            <li v-for="item in data">
                <input @input="check" type="checkbox" :value="item" v-model=value>
                <label class="checkbox-el__label" :for="item"> {{ item }} </label>
            </li>
        </ul>
        <div v-if="($v.value.$dirty && !$v.value.required)" class="error">{{error}}</div>
        <div v-else class="error"></div>
    </div>
</template>

<script>
import { validationMixin } from 'vuelidate';
import { required } from 'vuelidate/lib/validators';
export default {
    mixins: [validationMixin],
    name: 'register-block-checkbox-element',
    props: {
        title: String,
        data: Array,
        error: String,
    },
    data() {
        return {
            key: this.title,
            value: [],
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
    .checkbox-el {
        width: 49%;
        padding-right: 1rem;
        padding-left: 1rem;
        color: $clr-text;
        margin-bottom: 1rem;
        @include ff('Roboto', 1rem);

        & ul {
            list-style-type: none;
            padding-left: 0;
            & li {
                &:not(:last-child){
                    margin-bottom: .3rem;
                }

                @include ff('Roboto', 1rem, 300);
            
                & input {
                margin-left: 0;
                }
            }
        }
    }
</style>