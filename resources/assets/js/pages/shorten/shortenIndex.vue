<template>
  <div>
      <div class="md-layout md-gutter" :class="`md-alignment-center-center`">
         <form novalidate class="md-layout" @submit.prevent="validateUser">
            <md-card class="md-layout-item md-size-50 md-small-size-100">
               <md-card-content>
                  <div class="md-layout md-gutter">
                     <div class="md-layout-item md-small-size-100">
                        <md-field :class="getValidationClass('firstName')">
                           <label for="first-name">First Name</label>
                           <md-input name="first-name" id="first-name" autocomplete="given-name" v-model="form.firstName" :disabled="sending" />
                           <span class="md-error" v-if="!$v.form.firstName.required">The first name is required</span>
                           <span class="md-error" v-else-if="!$v.form.firstName.minlength">Invalid first name</span>
                        </md-field>
                     </div>
                  </div>
               </md-card-content>
            </md-card>
         </form>
      </div>
    </div>
</template>
<script>
import { validationMixin } from 'vuelidate'
import {
   required,
   email,
   minLength,
   maxLength
} from 'vuelidate/lib/validators'

export default {
  mixins: [validationMixin],
  mataInfo: () => {
     return {title: this.$t('shortenIndex')}
  },
  data: () => ({
   title: 'shortenIndex',
   form: {
      firstName: null,
      lastName: null,
      gender: null,
      age: null,
      email: null,
   },
   userSaved: false,
   sending: false,
   lastUser: null
  }),
  validations: {
      form: {
         firstName: {
            required,
            minLength: minLength(3)
         },
      // lastName: {
      // required,
      // minLength: minLength(3)
      // },
      // age: {
      // required,
      // maxLength: maxLength(3)
      // },
      // gender: {
      // required
      // },
      // email: {
      // required,
      // email
      // }
      }
   },
   methods: {
      getValidationClass (fieldName) {
        const field = this.$v.form[fieldName]

        if (field) {
          return {
            'md-invalid': field.$invalid && field.$dirty
          }
        }
      },
   }
}
</script>
