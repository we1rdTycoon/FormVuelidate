<template>

<div class="qqq">
  <form @submit.prevent="someAction()" class="form">
    <div class="field">
      <label for="name" class="required">Имя</label> <input name="name" :class="{ 'form-group--error': $v.name.$error }" type="text" v-model="name" @blur="$v.name.$touch()">
    </div>

    <div class="field">
      <label for="surname" class="required">Фамилия</label> <input name="surname" :class="{ 'form-group--error': $v.surname.$error }" type="text" v-model="surname" @blur="$v.surname.$touch()">
    </div>

    <div class="field">
      <label for="midllename" class="required">Отчество</label> <input name="midllename" :class="{ 'form-group--error': $v.midllename.$error }" type="text" v-model="midllename" @blur="$v.midllename.$touch()">
    </div>

    <div class="field">
     <label for="date" class="required">Дата рождения</label> <input name="date" :class="{ 'form-group--error': $v.date.$error }" type="text" v-model="date" @blur="$v.date.$touch()">
    </div>


    <div class="field">
      <label for="number" class="required">Номер телефона</label> <input name="number" :class="{ 'form-group--error': $v.number.$error }" type="text" v-model="number" @blur="$v.number.$touch()">
    </div>


    <div class="field">
    <label for="doctor" class="required">Лечащий врач</label>
     <select  name = "doctor" v-model="doctor" v-bind:class="{ 'form-group--error': $v.doctor.$invalid,'selects': !$v.doctor.$invalid,   }" >
			<option value = "Иванов">Иванов</option>
			<option value = "Захаров">Захаров</option>
			<option value = "Чернышева">Чернышева</option>
		</select>
    </div>

   <div class="field">
      <label>Отправлять СМС<input type="checkbox" v-model="sms"> </label>
    </div>
    

    <button type="submit" class="send" :disabled="$v.$invalid">
      Создать пользователя
    </button>

    <div class="field error">
      <div>
       <span v-if="$v.name.$error">
        <template v-if="!$v.name.required">
           Имя обязательно для заполнения
        </template>
        <template v-else>
          Имя должно содержать только буквы
        </template>
      </span>
      </div>

      <div>
      <span v-if="$v.surname.$error">
        <template v-if="!$v.surname.required">
          Отчество обязательно для заполнения
        </template>
        <template v-else>
          Отчество должно содержать только буквы
        </template>
      </span>
      </div>

      <div>
      <span v-if="$v.midllename.$error">
        <template v-if="!$v.midllename.required">
          Отчество обязательно для заполнения
        </template>
        <template v-else>
          Отчество должно содержать только буквы
        </template>
      </span>
      </div>

    <div>
      <span v-if="$v.date.$error">
        <template v-if="!$v.date.required">
          Дата обязательно для заполнения
        </template>
        <template v-else>
          Дата должна быть в формате ДД.ММ.ГГГГ
        </template>
      </span>
    </div>

    <div>
      <span v-if="$v.number.$error">
        <template v-if="!$v.number.required">
           Номер обязательный для заполнения
        </template>
        <template v-else>
          Неправильный формат номера
        </template>
      </span>
    </div>




    </div>


  </form>
  </div>
</template>

<script>
import { required, maxLength } from 'vuelidate/lib/validators';
import moment from 'moment';
export default {
  data() {
    return {
      name: null,
      surname:null,
      midllename:null,
      date:null,
      number:null,
      gender:null,
      doctor:null,
      sms:null,
    };
  },

  validations: {
    name: {
      required,
      alpha: val => /^[а-яё]*$/i.test(val),
    },
    surname: {
      required,
      alpha: val => /^[а-яё]*$/i.test(val),
    },
    midllename: {
      required,
      alpha: val => /^[а-яё]*$/i.test(val),
    },
    date: {
      required,
      validDate: val => moment(val, 'DD.MM.YYYY', true).isValid(),
    },
    number: {
      required,
      validNumber: val =>  /^(\+7|8)(\(\d{3}\)|\d{3})\d{7}$/.test(val),
    },
    doctor: {
      required,
    },
  },

  methods:{
    someAction: function(){
    
        alert("Пользователь создан");
      
    }
  }
};
</script>
<style>
body, html {
   height: 100%;
}
body{
  background: -webkit-linear-gradient(45deg, #EECFBA, #C5DDE8);
  display: flex;
  justify-content: center;
}

.qqq{
  margin-top: 50px;
  
}
.form{
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  padding: 20px;
  background: linear-gradient(90deg, #f598a8, #f6edb2);
border-radius: 10px;

}
.field{
  padding: 10px;
}
input, option {
   border: 2px solid #8ce8e3;
   font-family: 'Cutive Mono', monospace;
   transition: all .3s ease;
}
input:focus {
   outline:none;
   border: 2px solid #25c0b9;
}

label{
     font-family: 'Cutive Mono', monospace;
}
.send{
  align-self: center;
  font-weight: 700;
  color: white;
  text-decoration: none;
  padding: .8em 1em calc(.8em + 3px);
  border-radius: 3px;
  background: rgb(64,199,129);
  box-shadow: 0 -3px rgb(53,167,110) inset;
  transition: 0.2s;
  margin-top: 10px;
}

.send:hover{
 background: rgb(53, 167, 110);
}
span{
  color: red;
}
.error{
   align-self: center;
}
.form-group--error{
  border-color: red;
}

label.required:after
{
    color: red;
    content: "*";
}

.selects{
  border: 2px solid #8ce8e3;
   font-family: 'Cutive Mono', monospace;
   transition: all .3s ease;
}

</style>