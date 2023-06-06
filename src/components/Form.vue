<script lang="ts">

interface Form {
  firstName: string;
  lastName: string;
  email: string;
  phone: string;
  message: string;
  privacyPolicy: boolean;
}
export default {
  data() {
    return {
      form: {
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
        message: '',
        privacyPolicy: false
      } as Form,
      errors: {} as Record<string, string>
    };
  },
  methods: {
    submitForm() {
      this.resetErrors();
      if (this.validateForm()) {
        this.resetForm();
      }
    },
    validateForm() {
      let isValid = true;

      if (!this.form.firstName) {
        this.errors.firstName = 'Imię jest wymagane.';
        isValid = false;
      } else if (this.form.firstName.length > 32) {
        this.errors.firstName = 'Imię nie może być dłuższe niż 32 znaki.';
        isValid = false;
      }

      if (!this.form.lastName) {
        this.errors.lastName = 'Nazwisko jest wymagane.';
        isValid = false;
      } else if (this.form.lastName.length > 48) {
        this.errors.lastName = 'Nazwisko nie może być dłuższe niż 48 znaki.';
        isValid = false;
      }

      if (!this.isValidEmail(this.form.email)) {
        this.errors.email = 'Nieprawidłowy adres email.';
        isValid = false;
      }

      const phoneRegex = /^[0-9]{6,15}$/;
      if (!phoneRegex.test(this.form.phone)) {
        this.errors.phone = 'Nieprawidłowy numer telefonu.';
        isValid = false;
      }

      if (this.form.message.length > 250) {
        this.errors.message = 'Wiadomość nie może być dłuższa niż 250 znaków.';
        isValid = false;
      }

      if (!this.form.privacyPolicy) {
        this.errors.privacyPolicy = 'Musisz zaakceptować politykę prywatności.';
        isValid = false;
      }

      return isValid;
    },
    isValidEmail(email: string) {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      return emailRegex.test(email);
    },
    resetForm() {
      this.form = {
        firstName: '',
        lastName: '',
        email: '',
        phone: '',
        message: '',
        privacyPolicy: false
      };
    },
    resetErrors() {
      this.errors = {};
    }
  }
};

</script>

<template>
    <div>
      <h2>Formularz kontaktowy</h2>
      <form @submit.prevent="submitForm">

        <div>
          <label for="firstName">Imię:</label>
          <input type="text" id="firstName" v-model="form.firstName" />
          <span v-if="errors.firstName" class="error">{{ errors.firstName }}</span>
        </div>

        <div>
          <label for="lastName">Nazwisko:</label>
          <input type="text" id="lastName" v-model="form.lastName" />
          <span v-if="errors.lastName" class="error">{{ errors.lastName }}</span>
        </div>

        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="form.email" />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>

        <div>
          <label for="phone">Numer telefonu:</label>
          <input type="tel" id="phone" v-model="form.phone" />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>

        <div>
          <label for="message">Wiadomość:</label>
          <textarea id="message" v-model="form.message"></textarea>
          <span v-if="errors.message" class="error">{{ errors.message }}</span>
        </div>

        <div>
            
          <div class="check">
          <input type="checkbox" id="privacyPolicy" style="width: 20px;" v-model="form.privacyPolicy"/>
          <label for="privacyPolicy">Akceptuję politykę prywatności</label>
            
        </div>
        
        <div>
          <span v-if="errors.privacyPolicy" class="error">{{ errors.privacyPolicy }}</span>
        </div>

        </div>

        <button type="submit">Wyślij</button>

      </form>
    </div>
  </template>

<style scoped>

form{
  max-width: 500px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

textarea{
  max-width: 500px; 
  min-width: 500px;
  max-height: 300px;
  min-height: 50px;
}

button {
  margin: 0;
  padding: 0;
  border: none;
}

.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

h2 {
  font-size: 24px;
  margin-bottom: 20px;
  text-align: center;
}

label {
  display: block;
  margin-bottom: 5px;
  margin: 25px 0 15px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
textarea {
  display: block;
  width: 500px;
  padding: 10px 6px;
  box-sizing: border-box;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}

.check{
  display: flex;
}

button[type="submit"] {
  padding: 10px 20px;
  background-color: #007bff;
  color: #fff;
  border-radius: 4px;
  cursor: pointer;
  border: 0;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}

button[type="submit"]:hover {
  background-color: #0056b3;
}

</style>