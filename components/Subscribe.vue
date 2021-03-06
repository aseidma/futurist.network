<template>
  <div class="subscribe-container px-5 py-3">
    <div class="subscribe-container__cta d-flex align-items-center">
      <fa-icon class="fa-3x cta__icon" :icon="['fa', 'envelope']"></fa-icon>
      <div class="heading">Subscribe For<br />Weekly Updates</div>
    </div>

    <div class="subscribe-container__widget flex-col">
      <transition name="slide-fade" mode="out-in">      
      <b-form v-if="!userSubscribed" @submit.prevent="subscribeToNewsletter">
        <div class="widget__email-input d-flex align-items-center">
          <div class="email-input__input">
            <b-input
              v-model="email"
              class="form-control no-border"
              placeholder="Enter your email here."
              maxlength="50"
              type="email"
              required
              style="color: white; border-radius: 0;"
            />
          </div>
          <b-button type="submit" class="btn-subscribe">
            <fa-icon class="mr-2" :icon="['fa', 'paper-plane']"></fa-icon>
            <span class="btn-subscribe__text"> Subscribe </span>
          </b-button>
        </div>
        <b-button
          type="submit"
          :class="[
            'btn-subscribe--mobile',
            {'btn-subscribe--highlighted': email.length},
          ]"
        >
          <fa-icon class="mr-2" :icon="['fa', 'paper-plane']"></fa-icon>
          <span class="btn-subscribe__text"> Subscribe </span>
        </b-button>
        <p class="email-promise">
          * Your email is safe from spam and unsolicited sharing with us!
        </p>
      </b-form>
      <div v-else class="widget__success-message">
        <h3>You've subscribed!</h3>
      </div>
      </transition>
    </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: 'Subscribe',
  data() {
    return {
      email: '',
      userSubscribed: false
    }
  },
  methods: {
    async subscribeToNewsletter() {
      const response = await axios.get(`https://thefuturistfoundation.com/.netlify/functions/mailchimp-subscribe?email=${this.email}`)

      if (response.statusCode !== 200) {
        console.log("Something went wrong.")
      }

      this.userSubscribed = true
    },
  },
}
</script>

<style scoped>
/* General */
* {
  background-color: unset;
}

.subscribe-container {
  font-family: 'Montserrat', sans-serif;
  display: flex;
  align-items: center;
  margin: 1.25rem;
  background-color: #fe5c26;
  border-radius: 30px;
  color: white;
  min-height: 15rem;
}

/* CTA Section  */
.subscribe-container__cta {
  margin-right: 6rem;
  text-align: left;
}

.cta__icon {
  margin-right: 1rem;
}

.heading {
  font-weight: 700;
  color: white;
  font-size: 1.25rem;
  padding: 1.25rem 0;
  margin: 0;
}

/* Widget Section  */
.btn-subscribe--mobile {
  display: none;
}

.btn-subscribe {
  padding: 0.2rem 1rem;
}

.btn-subscribe:hover {
  color: #6c757d;
  background: none;
}

::placeholder {
  color: white;
}

.form-group {
  padding-top: 20px;
  text-align: left;
  margin: 0;
  width: auto;
}

.form-control {
  width: auto;
  padding: 0;
}

.form-control:focus {
  background-color: #fe5c26;
}

input:focus,
input.form-control:focus {
  outline: none 0 !important;
  box-shadow: none;
  -moz-box-shadow: none;
  -webkit-box-shadow: none;
}

.no-border {
  border: none;
}

.email-promise {
  font-size: 0.8rem;
}

.subscribe-container__widget {
  flex: 2;
  text-align: left;
}

.widget__email-input {
  justify-content: space-between;
  border-bottom: 2px solid;
  margin-bottom: 0.3rem;
}

.email-input__input {
  display: flex;
  align-items: center;
}

.widget__success-message {
  text-align: center;
}

/* Transitions */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
}

.slide-fade-enter,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(-5rem);
}

@media screen and (max-width: 540px) {
  /* General */
  .subscribe-container {
    flex-direction: column;
    min-height: 25rem;
  }

  /* CTA Section  */
  .subscribe-container__cta {
    margin: 0;
    flex-direction: column;
    text-align: center;
  }

  .cta__icon {
    margin: 0;
  }

  /* Widget Section  */
  .subscribe-container__widget {
    text-align: center;
    justify-content: center;
  }

  .widget__email-input {
    margin-bottom: 1rem;
  }

  .btn-subscribe {
    display: none;
  }

  .btn-subscribe--mobile {
    display: flex;
    align-items: center;
    padding: 0.8rem;
    margin: auto;
    margin-bottom: 1rem;
  }

  .btn-subscribe--highlighted {
    background-color: #6c757d;
  }

  .email-input__input {
    width: 100%;
  }

  .email-input__input input {
    text-align: center;
    width: 100%;
  }
}
</style>
