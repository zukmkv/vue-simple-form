<template>
    <div class="date-el">
        <label class="date-el__label" :for="title">
            <slot></slot>
        </label>
        <input @input="check" class="date-el__field" type="text" onfocus="(this.type='date')" min="1900-01-01" :max=max :name=title v-model="value">
        <div v-if="($v.value.$dirty && !$v.value.required)" class="error">{{error}}</div>
        <div v-else class="error"></div>
    </div>
</template>

<script>
import { validationMixin } from 'vuelidate';
import { required } from 'vuelidate/lib/validators';
export default {
    mixins: [validationMixin],
    name: 'register-block-date-element',
    props: ['title','error'],
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
    computed: {
        max: function () {
            const year = new Date().getFullYear();
            let month = new Date().getMonth();
            month++;
            if (month < 10) {
                month = '0' + month;
            }
            let day = new Date().getDate();
            if (day < 10) {
                day = '0' + day;
            }
            let today = `${year}-${month}-${day}`;
            return today;
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

    .date-el {
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