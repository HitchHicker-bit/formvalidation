<template>
  <div>
  <form class="home" @submit.prevent="submit">
      <div class="personality">
        <h1>Личные данные</h1>
        <div class="data-field">
          <div class="pers_data">
            <div class="field">
              <label>Имя*</label>
              <input class="personal" type="text" :class="{invalid: !$v.name.minLength || ($v.name.$dirty && !$v.name.required ||!$v.name.alpha), valid:($v.name.minLength && $v.name.required && $v.name.alpha)}" v-model.trim="name"/>
              <span class="error" v-if="$v.name.required && !$v.name.alpha">Здесь должны быть только буквы</span>
              <span class="error" v-if="$v.name.$dirty && !$v.name.required">Это поле не должны быть пустым!</span>
              <span class="error" v-else-if="!$v.name.minLength">Имя должно содержать больше {{$v.name.$params.minLength.min}} cимволов.</span>
            </div>
            <div class="field">
              <label>Фамилия*</label>
              <input class="personal" type="text" :class="{invalid: !$v.surname.minLength || (!$v.surname.required && $v.surname.$dirty || !$v.surname.alpha), valid:($v.surname.minLength && $v.surname.required && $v.surname.alpha)}" v-model.trim="surname"/>
              <span class="error" v-if="$v.surname.required && !$v.surname.alpha">Здесь должны быть только буквы</span>
              <span class="error" v-if="$v.surname.$dirty && !$v.surname.required">Это поле не должны быть пустым!</span>
              <span class="error" v-else-if="!$v.surname.minLength">Имя должно содержать больше {{$v.surname.$params.minLength.min}} cимволов.</span>
            </div>
            <div class="field">
              <label>Отчество</label>
              <input class="personal" :class="{valid:$v.patr.required}" type="text" v-model.trim="patr"/>
            </div>
            <div class="field">
              <label>Дата рождения*</label>
              <input class="personal" type="date" :class="{invalid:!$v.age.required && $v.age.$dirty , valid:$v.age.required}" v-model="age"/>
              <span class="error" v-if="!$v.age.required && $v.age.$dirty">Это поле не должны быть пустым!</span>
            </div>
          </div>
          <div class="pers_data_2">
            <div class="field">
              <label>Пол</label>
              <select class="personal" v-model="gender">
                <option>Мужской</option>
                <option>Женский</option>
                <option>Другой</option>
              </select>
            </div>
            <div class="field">
              <label>Группа клиентов*</label>
                <select class="personal" multiple v-model="typeCli">
                  <option>VIP</option>
                  <option>Проблемные</option>
                  <option>OMC</option>
                </select>
              <span class="error" v-if="typeChoosed">Вы должны выбрать хотя бы одну группу!</span>
            </div>
            <div class="field">
              <label>Лечащий врач</label>
              <select class="personal" v-model="doctor">
                <option>...</option>
                <option>Иванов</option>
                <option>Захаров</option>
                <option>Чернышева</option>
              </select>
            </div>
            <div class="field">
              <label>Номер телефона</label>
              <input class="personal" type="text" v-model.trim="phoneNumber" :class="{invalid:(!$v.phoneNumber.minLength && $v.phoneNumber.required && !$v.phoneNumber.russia), valid:$v.phoneNumber.required && $v.phoneNumber.minLength && $v.phoneNumber.russia}"/>
              <span class="error" v-if="!$v.phoneNumber.russia">Номер должен начинаться с 7</span>
              <span class="error" v-else-if="!$v.phoneNumber.minLength">Номер должен содержать 11 цифр</span>
            </div>
            <div class="field">
              <label>Не отправлять смс<input type="checkbox"/></label>
            </div>
          </div>
        </div>
      </div>
      <div class="geo_passport">
        <h1>Адрес и пасспортные данные</h1>
        <div class="data-field">
          <div class="pers_data">
            <div class="field">
              <label>Индекс</label>
              <input class="personal" type="text" :class="{invalid:!$v.index.numeric || ($v.index.required && !$v.index.minLength || !$v.index.maxLength), valid:($v.index.minLength && $v.index.required && $v.index.maxLength)}" v-model.trim="index"/>
              <span class="error" v-if="!$v.index.numeric">Здесь должны быть цифры</span>
              <span class="error" v-else-if="!$v.index.minLength || !$v.index.maxLength">Индекс должен быть из {{$v.index.$params.minLength.min}} цифр</span>
            </div>
            <div class="field">
              <label>Страна</label>
              <input class="personal" type="text" :class="{invalid: !$v.country.minLength, valid:$v.country.required && $v.country.minLength}" v-model.trim="country"/>
              <span class="error" v-if="!$v.country.minLength">Название должно быть не менее чем из {{$v.country.$params.minLength.min}} cимволов</span>
            </div>
            <div class="field">
              <label>Область</label>
              <input class="personal" :class="{invalid: !$v.region.minLength, valid:$v.region.required && $v.region.minLength}" type="text" v-model.trim="region"/>
              <span class="error" v-if="!$v.region.minLength">Название должно быть не менее чем из {{$v.region.$params.minLength.min}} cимволов</span>
            </div>
            <div class="field">
              <label>Город*</label>
              <input class="personal" type="text" :class="{invalid:$v.city.$dirty && !$v.city.required ||($v.city.required && !$v.city.minLength || !$v.city.alpha) , valid:$v.city.required && $v.city.minLength && $v.city.alpha}" v-model.trim="city"/>
              <span class="error" v-if="$v.city.required && !$v.city.alpha">Здесь должны быть только буквы</span>
              <span class="error" v-if="$v.city.required && !$v.city.minLength">Название должно быть не менее чем из {{$v.city.$params.minLength.min}} символов</span>
              <span class="error" v-else-if="$v.city.$dirty && !$v.city.required">Это поле не должны быть пустым!</span>
            </div>
            <div class="field">
              <label>Улица</label>
              <input class="personal" type="text" value='7' v-model.trim="street" :class="{invalid:$v.street.required && !$v.street.minLength, valid:$v.street.required && $v.street.minLength}"/>
              <span class="error" v-if="$v.street.required && !$v.street.minLength">Название должно быть не менее чем из {{$v.street.$params.minLength.min}} символов</span>
            </div>
            <div class="field">
              <label>Дом</label>
              <input class="personal" type="text" v-model.trim="house" :class="{invalid:($v.house.required && !$v.house.$dirty) || $v.house.required && !$v.house.between || !$v.house.numeric, valid:$v.house.required && $v.house.between && $v.house.numeric}">
              <span class="error" v-if="$v.house.required && !$v.house.numeric">Здесь должно быть число</span>
              <span class="error" v-if="$v.house.required && $v.house.numeric && !$v.house.between">Число должно быть от {{$v.house.$params.between.min}} до {{$v.house.$params.between.max}} </span>
            </div>
          </div>
          <div class="pers_data_2">
            <div class="field">
              <label>Тип документа*</label>
              <select class="personal" v-model="document">
                <option></option>
                <option>Пасспорт</option>
                <option>Свидетельство о рождении</option>
                <option>Вод.удостоверение</option>
              </select>
              <span class="error" v-if="!$v.document.required && $v.document.$dirty">Это поле не должны быть пустым!</span>
            </div>
            <div class="field">
              <label>Серия</label>
              <input class="personal" type="text" :class="{invalid:!$v.series.numeric || ($v.series.required && !$v.series.minLength || !$v.series.maxLength), valid:($v.series.minLength && $v.series.required && $v.series.maxLength)}" v-model.trim="series"/>
              <span class="error" v-if="!$v.series.minLength || !$v.series.maxLength">Серия пасспорта должна состоять из {{$v.series.$params.minLength.min}} цифр</span>
            </div>
            <div class="field">
              <label>Номер</label>
              <input class="personal" :class="{invalid:!$v.numberP.numeric || ($v.numberP.required && !$v.numberP.minLength || !$v.numberP.maxLength), valid:($v.numberP.required && $v.numberP.minLength && $v.numberP.maxLength)}" type="text" v-model.trim="numberP"/>
              <span class="error" v-if="!$v.numberP.minLength || !$v.numberP.maxLength">Номер пасспорта должен состоять из {{$v.numberP.$params.minLength.min}} цифр</span>
            </div>
            <div class="field">
              <label>Кем выдан</label>
              <input class="personal" type="text" :class="{invalid:$v.whoGive.required && !$v.whoGive.minLength , valid:$v.whoGive.required && $v.whoGive.minLength}" v-model="whoGive"/>
              <span class="error" v-if="!$v.whoGive.minLength">Имя того кем был выдан пасспорт {{$v.whoGive.$params.minLength.min}}</span>
            </div>
            <div class="field">
              <label>Дата выдачи</label>
              <input class="personal" type="date" v-model.trim="dateGot" :class="{invalid:!$v.dateGot.required && $v.dateGot.$dirty , valid:$v.dateGot.required}"/>
              <span class="error" v-if="!$v.dateGot.required && $v.dateGot.$dirty">Это поле не должно быть пустым</span>
            </div>
          </div>
        </div>
      </div>
      <div>
      <h2>*Поле обязательное для заполнения</h2>
      <button class="create">Создать</button>
      </div> 
  </form>
  </div>
</template>

<script>
import { required, minLength, between, numeric, helpers, maxLength } from 'vuelidate/lib/validators'
const russia = helpers.regex('russia', /^7/)
const alpha = helpers.regex('alpha', /^[A-zА-яЁё]+$/ )
export default {
  data() {
    return {
      name: '',
      surname:'',
      patr:'',
      age: '',
      typeCli:[],
      typeChoosed:false,
      gender:'',
      doctor:'',
      ageWrt:false,
      phoneNumber:'',
      index:'',
      country:'',
      region:'',
      city:'',
      street:'',
      document:'',
      series:'',
      numberP:'',
      whoGive:'',
      dateGot:'',
      house:'',
    }
  },
  watch:{
    'typeCli':{
      handler(val){
        if (val.length < 1){
          this.typeChoosed = true
        } else if (val.length > 0){
          this.typeChoosed = false
        }
      }
    }
  },
  validations: {
    name: {
      alpha,
      required,
      minLength: minLength(2)
    },
    surname:{
      alpha,
      required,
      minLength: minLength(4)
    },
    typeCli:{
      required
    },
    age:{
      required
    },
    patr:{
      required
    },
    doctor:{
      required
    },
    phoneNumber:{
      russia,
      required,
      minLength: minLength(11)
    },
    index:{
      numeric,
      required,
      minLength: minLength(6),
      maxLength: maxLength(6)
    },
    country:{
      required,
      minLength: minLength (3)
    },
    region:{
      required,
      minLength: minLength (5)
    },
    city:{
      alpha,
      required,
      minLength: minLength (4),
    },
    street:{
      required,
      minLength: minLength (4),
    },
    document:{
      required,
    },
    series:{
      numeric,
      required,
      minLength:minLength (4),
      maxLength:maxLength (4),
    },
    numberP:{
      numeric,
      required,
      minLength: minLength (6),
      maxLength: maxLength (6)
    },
    whoGive:{
      required,
      minLength: minLength (5)
    },
    dateGot:{ 
      required
    },
    house:{
      numeric,
      required,
      between: between(1, 100)
    }
  },
  methods: {
    submit() {
      console.log('submit!')
      const mainFields = [this.$v.age.$invalid, this.$v.surname.$invalid, this.$v.name.$invalid, this.$v.typeCli.$invalid, this.$v.city.$invalid, this.$v.document.$invalid, this.$v.dateGot.$invalid]
      const result = mainFields.filter(misstake => misstake == true);
      console.log(result.length)
      console.log(mainFields)
      this.$v.$touch()
      if (result.length > 0) {
        alert('Какие то из полей были неправильно заполнены!')
      } else {
        alert('Все поля заполнены правильно, клиент успешно создан!')
      }
      if (this.typeCli.length < 1){
        this.typeChoosed = true
      }
      
    },
  }
}
</script>
<style lang="sass">
.home
  position: absolute;
  top: 0
  left: 0
  width: 100%
  height: 100%
  display: flex
  justify-content: center
  flex-wrap: wrap

.personality
  width: 100%
  height: 100%
  display: flex
  flex-direction: column
  text-align: start
  margin-bottom: 10px

.geo_passport
  width: 100%
  height: 100%
  display: flex
  flex-direction: column
  text-align: start

.pers_data
  width: 35%
  height: 100%
  margin-left: 15% 
  display: flex
  flex-direction: column
  text-align: start

.pers_data_2
  width: 35%
  height: 100%
  margin-left: 15%
  display: flex
  flex-direction: column
  text-align: start

h1 
  color: #4acbfd
  text-align: center
  font-family: 'Rubik', sans-serif
label
  font-family: 'Rubik', sans-serif
  font-size: 20px

.field
  display: flex
  flex-direction: column
  height: 20%

.data-field
  display: flex
  width: 100%
  height: 80%
  flex-wrap: wrap
  justify-content: center
.create
  width: 100px
  border: none
  background: #4ACBFD
  border-radius: 10px
  color: white
  height: 50px
  font-size: 20px
.create:focus
  outline: none

@media only screen and (max-width: 420px)
  .home
    display: contents

  .personality
    width: 100%
    height: 100%
    display: flex
    flex-direction: column
    justify-content: center
    text-align: start

  .geo_passport
    width: 100%
    height: 100%
    display: flex
    flex-direction: column
    text-align: start

  .data-field
    display: flex
    flex-direction: column
    width: 100%
    height: 100%

  .pers_data
    width: 100%
    height: 100%
    display: flex
    flex-direction: column
    text-align: start

  h1 
    color: #4acbfd
    text-align: center
    font-family: 'Rubik', sans-serif

  .field
    display: flex
    flex-direction: column
    width: 80%
    height: 60px

  .personal
    border-top: none
    border-left: none
    border-right: none
    height: 20%
    width: 100%
    padding-top: 5px
    padding-bottom: 5px
    font-size: 8px
    font-family: 'Rubik', sans-serif
  label
    font-size: 10px
    font-family: 'Rubik', sans-serif
  .error
    color: red
    font-size: 8px     
    font-family: 'Rubik', sans-serif
  .create
    width: 50px
    border: none
    background: #4ACBFD
    border-radius: 10px
    color: white
    height: 25px
    font-size: 10px
  .create:focus
    outline: none
</style>
