<template>
<form v-on:submit.prevent="saveData">
    <div class="container">
        <register-block header="">
            <div class="row">
                <register-block-input-element title="surname" class="col-3" error="Поле не должно быть пустым!">Фамилия*</register-block-input-element>
                <register-block-input-element title="name" class="col-3" error="Поле не должно быть пустым!">Имя*</register-block-input-element>
                <register-block-input-element title="patronymic" class="col-3">Отчество</register-block-input-element>               
            </div>
            <div class="row">
                <register-block-select-element title="sex" class="col-3" :data="['','Мужской', 'Женский']">Пол</register-block-select-element>
                <register-block-date-element title="birthday" class="col-3" error="Укажите дату рождения">Дата рождения*</register-block-date-element>
                <register-block-input-phone-element title="phone-number" class="col-3" placeholder="79091234567" error="Некорректный ввод">Номер телефона*</register-block-input-phone-element>
            </div>
            <div class="row">
                <register-block-checkbox-element title="client" class="col-3" error="Необходимо выбрать категорию" :data="['VIP', 'Проблемные', 'ОМС']">Группа клиентов*</register-block-checkbox-element>
                <register-block-select-element title="doctor" class="col-2" :data="['','Иванов', 'Захаров', 'Чернышева']">Лечащий врач</register-block-select-element>
            </div>
            <div class="row">
                <register-block-checkbox-element title="sms" class="col-1" :data="['Не отправлять СМС']"></register-block-checkbox-element>
            </div>
        </register-block>
        <register-block header="Адрес регистрации">
            <div class="row">
                <register-block-input-element title="address-country" class="col-1">Страна</register-block-input-element>
            </div>
            <div class="row">
                <register-block-input-element title="address-region" class="col-1">Область</register-block-input-element>
            </div>
            <div class="row">
                <register-block-input-element title="address-city" class="col-1" error="Необходимо выбрать город">Город*</register-block-input-element>
            </div>
            <div class="row">
                <register-block-input-element title="address-street" class="col-3">Улица</register-block-input-element>
                <register-block-input-element title="address-house-number" class="col-3">Дом</register-block-input-element>
                <register-block-input-element title="address-index" class="col-3">Индекс</register-block-input-element>
            </div>
        </register-block>
        <register-block header="Документ, удостоверяющий личность">
            <div class="row">
                <register-block-select-element title="document-name" class="col-1" error="Не указан тип документа" :data="['Паспорт', 'Свидетельство о рождении', 'Вод. удостоверение']">Тип документа*</register-block-select-element>
            </div>
            <div class="row">
                <register-block-input-element title="document-series" class="col-3">Серия</register-block-input-element>
                <register-block-input-element title="document-number" class="col-3">Номер</register-block-input-element>
                <register-block-date-element title="document-data" class="col-3" error="Укажите дату выдачи">Дата выдачи*</register-block-date-element>
            </div>
            <div class="row">
                <register-block-input-element title="document-who" class="col-1">Кем выдан документ</register-block-input-element>
            </div>
            <div class="warning">* - поля, обязательные для заполнения</div>
        </register-block>
        <div class="msg">
            <span>
                {{message}}
            </span>
        </div>
        <register-button>Сохранить изменения</register-button>
    </div>
</form>
</template>

<script>
import RegisterBlock from './components/RegisterBlock';
import RegisterBlockInputElement from './components/RegisterBlockInputElement';
import RegisterBlockInputPhoneElement from './components/RegisterBlockInputPhoneElement';
import RegisterBlockSelectElement from './components/RegisterBlockSelectElement';
import RegisterBlockCheckboxElement from './components/RegisterBlockCheckboxElement';
import RegisterBlockDateElement from './components/RegisterBlockDateElement';
import RegisterButton from './components/RegisterButton';

export default {
    name: 'App',
    components: {
        RegisterBlock,
        RegisterBlockInputElement,
        RegisterBlockInputPhoneElement,
        RegisterBlockSelectElement,
        RegisterBlockCheckboxElement,
        RegisterBlockDateElement,
        RegisterButton,
    },
    data() {
        return {
            message: '',
            surname: {
                value: '',
            }, 
            name: {
                value: '',
            },
            patronymic: '',
            sex: '',
            birthday: {
                value: '',
            },
            'phone-number': {
                value: '',
            },
            client: {
                value: [],
            },
            doctor: '',
            sms: [],
            'address-country': '',
            'address-region': '',
            'address-city': {
                value: '',
            },
            'address-street': '',
            'address-house-number': '',
            'address-index': '',
            'document-name': {
                value: '',
            },
            'document-series': '',
            'document-number': '',
            'document-data': {
                value: '',
            },
            'document-who': '',
        }
    },
    methods: {
        saveData: function(){
            let array = [];
            array.push(this.$children[0].$children[0].$v.$invalid);
            array.push(this.$children[0].$children[1].$v.$invalid);
            array.push(this.$children[0].$children[4].$v.$invalid);
            array.push(this.$children[0].$children[5].$v.$invalid);
            array.push(this.$children[0].$children[6].$v.$invalid);
            array.push(this.$children[1].$children[2].$v.$invalid);
            array.push(this.$children[2].$children[0].$v.$invalid);
            array.push(this.$children[2].$children[3].$v.$invalid);
            let noInvalid = array.every( value => value === false);
            if (noInvalid) {
                this.message = 'Аккаунт успешно создан';
            } else {
                this.message = 'Пожалуйста, заполните необходимые поля'
            }
            return noInvalid;
        }
    },
}
</script>

<style lang="scss">
    @import "./styles/general";
    .container {
        @media screen and (max-width: 544px){
            max-width: 100%;
        }
        @media screen and (min-width: 544px) and (max-width: 974px){
            width: 33rem;
        }
        @media screen and (min-width: 975px) and (max-width: 1184px){
            width: 45rem;
        }
        @media screen and (min-width: 1185px){
            width: 51rem;
        }
        width: 52rem;
        height: auto;
        background-color: whitesmoke;
        margin: auto;
        margin-top: 0;

    }

    .row {
        display: flex;
        flex-wrap: wrap;
        &:first-of-type {
            padding-top: 1rem;
        }
    }
    .warning {
        padding: 0 0 1rem 1rem;
        @include ff('Roboto', .8rem);
    }

    .msg {
        padding: 0 0 1rem 1rem;
        @include ff('Roboto', 1rem, bold);
    }
</style>

