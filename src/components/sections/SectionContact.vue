<template>
    <div class="contact-wrapper">
        <div class="main-info">
            <p class="contact-text">ПРЕДСТАВТЕСЯ, БУДЬ ЛАСКА</p>
            <div class="contact-input-wrapper">
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.lastName ? 'black' : 'red'}">* ПРІЗВИЩЕ</p>
                    <input type="text" v-model="form.lastName" :style="{border: `1px solid ${formValidation.lastName ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.firstName ? 'black' : 'red'}">* ІМ'Я</p>
                    <input type="text" v-model="form.firstName" :style="{border: `1px solid ${formValidation.firstName ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.organization ? 'black' : 'red'}">ОРГАНІЗАЦІЯ ТА ПОСАДА</p>
                    <input type="text" v-model="form.organization" :style="{border: `1px solid ${formValidation.organization ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input-radio">
                    <input type="radio" v-model="form.role" value="consumer">
                    <p class="input-radio-label">СПОЖИВАЧ</p>
                </div>
                <div class="contact-input-radio">
                    <input type="radio" v-model="form.role" value="worker">
                    <p class="input-radio-label">МЕДИЧНИЙ ПРАЦІВНИК</p>
                </div>
                <div class="contact-input-radio">
                    <input type="radio" v-model="form.role" value="journalist">
                    <p class="input-radio-label">ЖУРНАЛІСТ</p>
                </div>
                <p class="contact-message-text">ПОВІДОМЛЕННЯ</p>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.subject ? 'black' : 'red'}">ТЕМА ПОВІДОМЛЕННЯ</p>
                    <input type="text" v-model="form.subject" :style="{border: `1px solid ${formValidation.subject ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.message ? 'black' : 'red'}">* ПОВІДОМЛЕННЯ</p>
                    <textarea type="text" v-model="form.message" :style="{border: `1px solid ${formValidation.message ? 'black' : 'red'}`}"></textarea>
                </div>
            </div>
        </div>
        <div class="contact-info">
            <p class="contact-text">КОНТАКТНА ІНФОРМАЦІЯ</p>
            <div class="contact-input-wrapper">
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.email ? 'black' : 'red'}">* EMAIL</p>
                    <input type="text" v-model="form.email" :style="{border: `1px solid ${formValidation.email ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.country ? 'black' : 'red'}">КРАЇНА</p>
                    <input type="text" v-model="form.country" :style="{border: `1px solid ${formValidation.country ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.city ? 'black' : 'red'}">МІСТО</p>
                    <input type="text" v-model="form.city" :style="{border: `1px solid ${formValidation.city ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.postalCode ? 'black' : 'red'}">ІНДЕКС</p>
                    <input type="text" v-model="form.postalCode" :style="{border: `1px solid ${formValidation.postalCode ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.address ? 'black' : 'red'}">АДРЕСА</p>
                    <input type="text" v-model="form.address" :style="{border: `1px solid ${formValidation.address ? 'black' : 'red'}`}">
                </div>
                <div class="contact-input">
                    <p class="input-label" :style="{color: formValidation.phone ? 'black' : 'red'}">* ТЕЛЕФОН</p>
                    <input type="text" placeholder="(xxx) xxx-xx-xx" v-model="form.phone" @input="formatPhone" :style="{border: `1px solid ${formValidation.phone ? 'black' : 'red'}`}">
                </div>
            </div>
            <div class="button-send-contact" @click="sendRequest">відправити</div>
        </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    name: "SectionContact",
    setup() {
      const form = ref({
        lastName: '',
        firstName: '',
        organization: '',
        role: 'consumer',
        email: '',
        country: '',
        city: '',
        postalCode: '',
        address: '',
        phone: '',
        subject: '',
        message: ''
      });
      const formValidation = ref({
        lastName: true,
        firstName: true,
        organization: true,
        email: true,
        country: true,
        city: true,
        postalCode: true,
        address: true,
        phone: true,
        subject: true,
        message: true
      })
      const formatPhone = () => {
        let input = form.value.phone.replace(/\D/g, '');
        input = input.substring(0, 10);

        if (input.length > 0) {
            input = '(' + input;
        }
        if (input.length > 4) {
            input = input.slice(0, 4) + ') ' + input.slice(4);
        }
        if (input.length > 9) {
            input = input.slice(0, 9) + '-' + input.slice(9);
        }
        if (input.length > 12) {
            input = input.slice(0, 12) + '-' + input.slice(12, 14);
        }

        form.value.phone = input;
      }
      const validateForm = () => {
        let valid = true;

        if (!(form.value.lastName.length > 0) || !/^[\u0400-\u04FF]+$/.test(form.value.lastName)) {
          valid = false;
          formValidation.value.lastName = false;
        } else {
          formValidation.value.lastName = true;
        }
        if (!(form.value.firstName.length > 0) || !/^[\u0400-\u04FF]+$/.test(form.value.firstName)) {
          valid = false;
          formValidation.value.firstName = false;
        } else {
          formValidation.value.firstName = true;
        }
        if (!/^[\u0400-\u04FF]*$/.test(form.value.organization)) {
          valid = false;
          formValidation.value.organization = false;
        } else {
          formValidation.value.organization = true;
        }
        if (!/^[\u0400-\u04FF]*$/.test(form.value.country)) {
          valid = false;
          formValidation.value.country = false;
        } else {
          formValidation.value.country = true;
        }
        if (!/^[\u0400-\u04FF]*$/.test(form.value.city)) {
          valid = false;
          formValidation.value.city = false;
        } else {
          formValidation.value.city = true;
        }
        if (!/^\d*$/.test(form.value.postalCode)) {
          valid = false;
          formValidation.value.postalCode = false;
        } else {
          formValidation.value.postalCode = true;
        }
        if (!/^[\u0400-\u04FF0-9/,\- ]*$/.test(form.value.address)) {
          valid = false;
          formValidation.value.address = false;
        } else {
          formValidation.value.address = true;
        }
        if (!(form.value.phone.replace(/\D/g, '').length > 0) || !/^\d{10}$/.test(form.value.phone.replace(/\D/g, ''))) {
          valid = false;
          formValidation.value.phone = false;
        } else {
          formValidation.value.phone = true;
        }
        if (!/^[\u0400-\u04FF0-9]*$/.test(form.value.subject)) {
          valid = false;
          formValidation.value.subject = false;
        } else {
          formValidation.value.subject = true;
        }
        if (!(form.value.message.length > 0) || !/^[\u0400-\u04FF0-9]+$/.test(form.value.message)) {
          valid = false;
          formValidation.value.message = false;
        } else {
          formValidation.value.message = true;
        }
        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.value.email)) {
          valid = false;
          formValidation.value.email = false;
        } else {
          formValidation.value.email = true;
        }
        return valid
      }
      const sendRequest = () => {
        if (validateForm()) alert("Успішно відправлено!")
      }
      return {
        form,
        formValidation,
        formatPhone,
        validateForm,
        sendRequest
      };
    }
  };
  </script>
  
  <style scoped>
  .contact-wrapper {
    display: flex;
    justify-content: center;
    gap: 150px;
  }
  .contact-info {
    min-width: 250px;
    position: relative
  }
  .main-info {
    min-width: 250px;
  }
  .contact-text {
    font-size: 18px;
  }
  .contact-input-wrapper {
    display: flex;
    flex-direction: column;
    gap: 15px;
    margin-top: 50px;
  }
  .input-label {
    font-size: 12px;
    margin-bottom: 3px;
  }
  .contact-input-radio {
    display: flex;
    align-items: center;
    gap: 5px;
    font-size: 12px;
  }
  .contact-input-radio input {
    margin: 0;
  }
  .input-radio-label {
    margin-top: 4px;
  }
  .contact-input input {
    width: 100%;
    height: 31px;
  }
  .contact-input textarea {
    resize: none;
    width: 100%;
    height: 85px;
  }
  .contact-message-text {
    font-size: 18px;
    margin-top: 25px;
    margin-bottom: 10px;
  }
  .button-send-contact {
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    bottom: 0;
    padding: 5px 0;
    border: 1px solid black;
    width: 100%;
    background-color: #464646;
    color: white;
    font-size: 20px;
  }
  .button-send-contact:hover {
    cursor: pointer;
  }
  @media screen and (max-width: 768px) {
    .contact-wrapper {
        flex-direction: column;
        padding: 0 100px;
    }
    .contact-wrapper {
      gap: 25px;
      align-items: center;
    }
    .button-send-contact {
      position: unset;
      margin-top: 15px;
    }
    .contact-input-wrapper {
      margin-top: 25px;
    }
    
  }
  </style>
  