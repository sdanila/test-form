<template>
  <form id="form" class="form" @submit.prevent="onSubmit">
    <h3 class="form__title">Данные пациента</h3>
    <section class="fio">

      <label class="form__label required">Имя:
        <input
          type="text"
          class="form__input"
          id="firstName"
          v-model.trim="firstName"
          :class="{invalid: ($v.firstName.$dirty && !$v.firstName.required)}"
        >
        <small
          class="invalid"
          v-if="($v.firstName.$dirty && !$v.firstName.required)"
        >
          Поле обязательное для заполнения
        </small>
      </label>

      <label class="form__label required">Фамилия:
        <input
          type="text"
          class="form__input"
          id="lastName"
          :class="{invalid: ($v.lastName.$dirty && !$v.lastName.required)}"
          v-model.trim="lastName"
        >
        <small
          class="invalid"
          v-if="($v.lastName.$dirty && !$v.lastName.required)"
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
          :class="{invalid: ($v.dateborn.$dirty && !$v.dateborn.required)}"
          v-model.trim="dateborn"
        >
        <small
          class="invalid"
          v-if="$v.dateborn.$dirty && !$v.dateborn.required"
        >
          Поле обязательное для заполнения
        </small>
      </label>

      <label class="form__label required">Номер телефона:
        <input
          type="tel"
          class="form__input"
          id="phone"
          v-model.trim="phone"
          :class="{invalid: ($v.phone.$dirty && !$v.phone.required) || ($v.phone.$dirty && !$v.phone.minLength) || ($v.phone.$dirty && !$v.phone.maxLength)}"
        >
        <small
          class="invalid"
          v-if="$v.phone.$dirty && !$v.phone.required"
        >
          Поле обязательное для заполнения
        </small>

        <small
          class="invalid"
          v-else-if="($v.phone.$dirty && !$v.phone.minLength) || ($v.phone.$dirty && !$v.phone.maxLength)"
        >
          Номер должен содержать {{$v.phone.$params.minLength.min}} цифр. <br> Сейчас он {{phone.length}}
        </small>

        <!-- <small
          class="helper-text invalid"
          v-else-if="$v.password.$dirty && !$v.password.minLength"
        >
          Пароль должен быть {{$v.password.$params.minLength.min}} символов. Сейчас он {{password.length}}
        </small> -->



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
          :class="{invalid: ($v.group.$dirty && !$v.group.required)}"
          v-model="group"
        >
          <option value="vip">VIP</option>
          <option value="Propblem">Проблемные</option>
          <option value="insurance">ОМС</option>
        </select>
        <small
          class="invalid"
          v-if="($v.group.$dirty && !$v.group.required)"
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
          v-model="sms"
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
          :class="{invalid: ($v.city.$dirty && !$v.city.required)}"
          v-model="city"
        >
        <small
          class="invalid"
          v-if="($v.city.$dirty && !$v.city.required)"
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
            :class="{invalid: ($v.document.$dirty && !$v.document.required)}"
            v-model="document"
          >
            <option value="pasport">Паспорт</option>
            <option value="birth-certificate">Свидетельство о рождении</option>
            <option value="drivers-license">Водительское удостоверение</option>
          </select>
        </div>
        <small
          class="invalid"
          v-if="($v.document.$dirty && !$v.document.required)"
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
          :class="{invalid: ($v.dateIssued.$dirty && !$v.dateIssued.required)}"
          v-model="dateIssued"
        >
        <small
          class="invalid"
          v-if="($v.dateIssued.$dirty && !$v.dateIssued.required)"
        >
          Поле обязательное для заполнения
        </small>
      </label>
    </section>

    <button type="submit" class="form__submit">Создать</button>
  </form>
</template>

<script>
import { required, minLength, maxLength } from 'vuelidate/lib/validators'

export default {
  name: 'Form',
  data: () => ({
    firstName: '',
    lastName: '',
    patronymic: '',
    dateborn: null,
    phone: null,
    gender: '',
    group: [],
    doctor: '',
    sms: false,
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
    submitStatus: '',
  }),
  validations: {
    firstName: { required },
    lastName: { required },
    phone: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
    },
    dateborn: { required },
    group: { required },
    city: { required },
    document: { required },
    dateIssued: { required },
  },
  methods: {
    onSubmit() {
      if (this.$v.$invalid) {
        this.$v.$touch();
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
        sms: this.sms,
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
    }
  }
}
</script>

<style lang="sass">
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
    width: 98%
    border-radius: 5px
    padding: 3px
    padding-left: 10px
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

@media (max-width: 991px)
  .form__label
    width: 28%
@media (max-width: 767px)
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
      width: 95%
    &__checkbox
      margin-top: 2px
    &__textarea
      width: 96%
    &__submit
      width: 50%
      padding: 0
      bottom: 45px
      right: 50%
      transform: translateX(50%)
      font-size: 16px
      height: 30px
</style>