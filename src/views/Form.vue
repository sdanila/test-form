<template>
  <div class="container">
    <form id="form" class="form" @submit.prevent="onSubmit">
      <h3 class="form__title">Данные пациента</h3>
      <section class="fio">

        <label class="form__label required">Имя:
          <input
            type="text"
            class="form__input"
            id="firstName"
            v-model.trim="firstName"
            :class="{invalid: validFirstName}"
          >
          <small
            class="invalid"
            v-if="validFirstName"
          >
            Поле обязательное для заполнения
          </small>
        </label>

        <label class="form__label required">Фамилия:
          <input
            type="text"
            class="form__input"
            id="lastName"
            :class="{invalid: validLastName}"
            v-model.trim="lastName"
          >
          <small
            class="invalid"
            v-if="validLastName"
          >
            Поле обязательное для заполнения
          </small>
        </label>

        <label class="form__label">Отчество:
          <input
            type="text"
            class="form__input"
            id="patronymic"
            v-model.trim="patronymic"
          >
        </label>

        <label class="form__label required">Дата рождения:
          <input
            type="date"
            class="form__input"
            id="dateborn"
            :class="{invalid: validDateborn}"
            v-model="dateborn"
          >
          <small
            class="invalid"
            v-if="validDateborn"
          >
            Поле обязательное для заполнения
          </small>
        </label>

        <label class="form__label required">Номер телефона:
          <input
            type="number"
            class="form__input"
            id="phone"
            placeholder='Должен начинаться с цифры "7"'
            v-model.trim="phone"
            :class="{invalid: validPhone}"
          >
          <small
            class="invalid"
            v-if="validPhoneRequired"
          >
            Поле обязательное для заполнения
          </small>


          <small
            class="invalid"
            v-else-if="validPhoneMLength"
          >
            Номер должен содержать {{$v.phone.$params.minLength.min}} цифр. <br>
            Сейчас: {{phone.length}}.
          </small>

          <small
            class="invalid"
            v-else-if="validPhoneNumber"
          >
            Номер должен начинаться с цифры "7"
          </small>
        </label>

        <label class="form__label">Пол:
          <div class="wrapper">
            <select id="gender" class="form__select" v-model="gender" >
              <option value="male" selected>Мужчина</option>
              <option value="female">Женщина</option>
            </select>
          </div>
        </label>

        <label class="form__label required">Группа пациентов:
          <select
            id="group"
            class="form__select form__select_group"
            multiple
            :class="{invalid: validGroup}"
            v-model="group"
          >
            <option value="vip">VIP</option>
            <option value="Propblem">Проблемные</option>
            <option value="insurance">ОМС</option>
          </select>
          <small
            class="invalid"
            v-if="validGroup"
          >
            Поле обязательное для заполнения
          </small>
        </label>

        <label class="form__label">Лечащий врач:
          <div class="wrapper">
            <select
              id="doctor"
              class="form__select form__select_doctor"
              v-model="doctor"
            >
              <option value="Ivanov">Иванов</option>
              <option value="Zaharov">Захаров</option>
              <option value="Сhernysheva">Чернышева</option>
            </select>
          </div>
        </label>

        <label class="form__label form__label_checkbox">Не отправлять смс:
          <input
            type="checkbox"
            id="sms"
            class="form__checkbox"
            v-model="noSms"
          >
        </label>

      </section>

      <hr>

      <h3 class="form__title">Адрес:</h3>
      <section class="adress">
        <label class="form__label form__label_mb-0">Индекс:
          <input
            type="number"
            class="form__input"
            id="index"
            v-model="index"
          >
        </label>

        <label class="form__label form__label_mb-0">Страна:
          <input
            type="text"
            class="form__input"
            id="country"
            v-model="country"
          >
        </label>

        <label class="form__label form__label_mb-0">Область:
          <input
            type="text"
            class="form__input"
            id="region"
            v-model="region"
          >
        </label>

        <label class="form__label form__label_mb-0 required">Город:
          <input
            type="text"
            class="form__input"
            id="city"
            :class="{invalid: validCity}"
            v-model="city"
          >
          <small
            class="invalid"
            v-if="validCity"
          >
            Поле обязательное для заполнения
          </small>
        </label>

        <label class="form__label form__label_mb-0">Улица:
          <input
            type="text"
            class="form__input"
            id="street"
            v-model="street"
          >
        </label>

        <label class="form__label form__label_mb-0">Дом:
          <input
            type="text"
            class="form__input"
            id="house"
            v-model="house"
          >
        </label>
      </section>

      <hr>

      <h3 class="form__title">Паспорт:</h3>
      <section class="typeDocument">

        <label class="form__label required">Тип документа:
          <div class="wrapper">
            <select
              id="document"
              class="form__select"
              :class="{invalid: validDocument}"
              v-model="document"
            >
              <option value="pasport">Паспорт</option>
              <option value="birth-certificate">Свидетельство о рождении</option>
              <option value="drivers-license">Водительское удостоверение</option>
            </select>
          </div>
          <small
            class="invalid"
            v-if="validDocument"
          >
            Поле обязательное для заполнения
          </small>
        </label>

        <label class="form__label form__label_mb-10">Серия:
          <input
            type="text"
            class="form__input"
            id="document-series"
            v-model="documentSeries"
          >
        </label>

        <label class="form__label form__label_mb-10">Номер:
          <input
            type="text"
            class="form__input"
            id="document-number"
            v-model="documentNumber"
          >
        </label>

        <label class="form__label form__label_mb-10">Кем выдан:
          <textarea
            id="issued-by"
            class="form__textarea"
            v-model="issuedBy"
          ></textarea>
        </label>

        <label class="form__label form__label_mb-10 required">Дата выдачи:
          <input
            type="date"
            class="form__input"
            id="date-issued"
            :class="{invalid: validDateIssued}"
            v-model="dateIssued"
          >
          <small
            class="invalid"
            v-if="validDateIssued"
          >
            Поле обязательное для заполнения
          </small>
        </label>
      </section>

      <button type="submit" class="form__submit">Создать</button>
      <span class="annotation">(<small>✱</small>) - Поле обязательное для заполнения</span>
    </form>
    <template v-if="alert">
      <Alert :msg="alertMsg" :className="alertClass" />
    </template>
  </div>
</template>

<script>
import { required, minLength, maxLength } from 'vuelidate/lib/validators';
import Alert from '../components/Alert';

const numberValidation = (value) => {
  const num = value.split('');
  console.log(num)
  if (num[0] !== "7") {
    return false
  }
  return true
}

export default {
  name: 'Form',
  components: {
    Alert,
  },
  data: () => ({
    firstName: '',
    lastName: '',
    patronymic: '',
    dateborn: null,
    phone: null,
    gender: '',
    group: [],
    doctor: '',
    noSms: false,
    index: '',
    country: '',
    region: '',
    city: '',
    street: '',
    house: null,
    document: '',
    documentSeries: '',
    documentNumber: '',
    issuedBy: '',
    dateIssued: null,
    alert: false,
    alertMsg: '',
    alertClass: '',
  }),
  validations: {
    firstName: { required },
    lastName: { required },
    phone: {
      required,
      numberValidation,
      minLength: minLength(11),
      maxLength: maxLength(11),
    },
    dateborn: { required },
    group: { required },
    city: { required },
    document: { required },
    dateIssued: { required },
  },
  computed: {
    validFirstName() {
      return this.$v.firstName.$dirty && !this.$v.firstName.required
    },
    validLastName() {
      return this.$v.lastName.$dirty && !this.$v.lastName.required
    },
    validDateborn() {
      return this.$v.dateborn.$dirty && !this.$v.dateborn.required
    },
    validGroup() {
      return this.$v.group.$dirty && !this.$v.group.required
    },
    validCity() {
      return this.$v.city.$dirty && !this.$v.city.required
    },
    validDocument() {
      return this.$v.document.$dirty && !this.$v.document.required
    },
    validDateIssued() {
      return this.$v.dateIssued.$dirty && !this.$v.dateIssued.required
    },
    validPhoneRequired() {
      return this.$v.phone.$dirty && !this.$v.phone.required
    },
    validPhoneMLength() {
      return (this.$v.phone.$dirty && !this.$v.phone.minLength) ||
            (this.$v.phone.$dirty && !this.$v.phone.maxLength)
    },
    validPhoneNumber() {
      return this.$v.phone.$dirty && !this.$v.phone.numberValidation
    },
    validPhone() {
      return (this.$v.phone.$dirty && !this.$v.phone.required) ||
            (this.$v.phone.$dirty && !this.$v.phone.minLength) ||
            (this.$v.phone.$dirty && !this.$v.phone.maxLength) ||
            (this.$v.phone.$dirty && !this.$v.phone.numberValidation)
    },
  },
  methods: {
    onSubmit() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        console.log(this.$v)
        this.alert = true;
        this.alertMsg = 'Не отправлено.  Проверьте все поля.';
        this.alertClass = 'error';
        setTimeout(() => {
          this.alert = false;
        }, 5000);
        return
      }
      const post = {
        firstName: this.firstName,
        lastName: this.lastName,
        patronymic: this.patronymic,
        dateborn: this.dateborn,
        phone: this.phone,
        gender: this.gender,
        group: this.group,
        doctor: this.doctor,
        noSms: this.noSms,
        index: this.index,
        country: this.country,
        region: this.region,
        city: this.city,
        street: this.street,
        house: this.house,
        document: this.document,
        documentSeries: this.documentSeries,
        documentNumber: this.documentNumber,
        issuedBy: this.issuedBy,
        dateIssued: this.dateIssued,
      };
      console.log(post);
      this.alert = true;
      this.alertMsg = 'Отправлено';
      this.alertClass = 'success';
      setTimeout(() => {
        this.alert = false;
      }, 5000);
    }
  }
}
</script>

<style lang="sass">
.container
  margin: 0 auto
  width: 960px
.form
  position: relative
  background: rgb(48, 152, 178)
  padding: 15px 30px
  margin: 0 auto
  border-radius: 5px
  min-height: 510px
  &__title
    color: #fff
  &__label
    width: 30%
    display: block
    color: white
    margin-bottom: 15px
    border-radius: 5px
    margin-right: 45px
    &_checkbox
      display: flex
    &_mb-0
      margin-bottom: 0
    &_mb-10
      margin-bottom: 10px
  &__label:nth-child(3n)
    margin-right: 0
  &__label:nth-child(9)
    cursor: pointer
  &__input
    border: none
    width: 95%
    border-radius: 5px
    padding: 3px
    padding-left: 10px
  &__input::placeholder
    font-size: 10px
  &__select
    position: relative
    border: none
    width: 100%
    border-radius: 5px
    padding: 3px
    -webkit-appearance: none
    -moz-appearance: none
    appearance: none
    cursor: pointer
    &_group
      height: 65px
  .wrapper
    position: relative
    cursor: pointer
  .wrapper:after
    content: "⏷"
    color: #0e95b6
    position: absolute
    font-size: 14px
    right: 1%
    top: 6%
    pointer-events: none
    opacity: 1
  &__textarea
    width: 97%
    height: 55px
    padding: 5px
    border: none
    border-radius: 5px
    resize: none
  &__checkbox
    -webkit-appearance: none
    -moz-appearance: none
    appearance: none
    width: 16px
    margin-left: 10px
    height: 16px
    position: relative
    border-radius: 4px
    background-color: white
    cursor: pointer
    border: 1px solid #d6d6cd
  &__checkbox::before
    content: "✔"
    color: #0e95b6
    font-size: 18px
    position: absolute
    right: 50%
    bottom: 50%
    transform: translate(50%, 50%)
    opacity: 0
    cursor: pointer
    transition: .1s ease-in
  &__checkbox:checked::before
    opacity: 1
  &__submit
    position: absolute
    bottom: 15px
    right: 30px
    border-radius: 5px
    background-color: #fff
    color: #0e758e
    font-size: 14px
    border: none
    height: 24px
    width: 13%
    text-transform: uppercase
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button
    -webkit-appearance: none
    margin: 0
  input[type=number]
    -moz-appearance: textfield
  .fio,
  .adress,
  .typeDocument
    display: flex
    flex-wrap: wrap
    justify-content: flex-start
  .fio
    min-height: 160px
  .adress
    display: flex
    flex-wrap: wrap
    min-height: 120px
    justify-content: flex-start
  .typeDocument
    min-height: 120px
    margin-bottom: 10px
  .required
    position: relative
  .required::after
    content: "✱"
    color: #dc0f0f
    font-size: 11px
    position: absolute
    left: -13px
    top: -4px
    opacity: 1
  .invalid
    border: 2px solid #dc0f0f
  small.invalid
    border: none
    color: #a22424
  .annotation
    position: absolute
    top: 13px
    right: 14px
    color: white
    font-size: 11px
    small
      color: #dc0f0f
@media (min-width: 1216px)
  .container
    width: 80%
@media (max-width: 991px)
  .container
    width: 720px
  .form
    &__label
      width: 28%
    &__input
      width: 92%
@media (max-width: 767px)
  .container
    width: 540px
  .form
    padding-bottom: 50px
    &__label
      font-size: 15px
      width: 44%
      margin: 0
      margin-bottom: 10px
    &__label:nth-child(odd)
      margin-right: 56px
    &__label:nth-child(9)
      margin-right: 0
      margin-left: 64%
    &__input
      width: 94%
      height: 20px
    &__select
      height: 26px
      &_group
        height: 65px
    &__checkbox
      margin-top: 4px
    &__textarea
      width: 95%
    &__submit
      width: 27%
      bottom: 50px
      font-size: 17px
      height: 35px
@media (max-width: 574px)
  .container
    width: 100%
  .form
    padding-bottom: 90px
    &__label
      margin-right: 0
      width: 100%
      &_mb-10, &_mb-0
        margin-bottom: 15px
    &__label:nth-child(odd)
      margin-right: 0
    &__label:nth-child(9)
      margin-left: 0
      margin-top: 10px
    &__input
      height: 25px
      width: 96%
    &__checkbox
      margin-top: 2px
    &__textarea
      width: 97%
    &__submit
      width: 50%
      padding: 0
      bottom: 45px
      right: 50%
      transform: translateX(50%)
      font-size: 16px
      height: 30px
    .annotation
      font-size: 10px
      top: 10px
</style>