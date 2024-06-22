<template>
<b-container class="bv-example-row">
  <b-row>
    <b-col></b-col>
    <b-col><div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <!-- input EmailAddress -->
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>
      <!-- input EmailAddress -->

      <!-- input Password -->
      <b-form-group
        id="input-group-2"
        label="Password:"
        label-for="input-2"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-2"
          v-model="form.password"
          type="password"
          placeholder="Enter Password"
          required
        ></b-form-input>
      </b-form-group>
      <!-- input Password -->      

      <!-- random checkbox -->
      <b-form-group id="input-group-4" v-slot="{ ariaDescribedby }">
        <b-form-checkbox-group
          v-model="form.checked"
          id="checkboxes-4"
          :aria-describedby="ariaDescribedby"
        >
          
        </b-form-checkbox-group>
      </b-form-group>
      <!-- random checkbox -->

      <!-- Sign Up / Submit button -->
      <b-button type="button" variant="primary" @click="register()">Sign Up</b-button>
      
    </b-form>
    
  </div></b-col>
    <b-col></b-col>
  </b-row>
</b-container>
  
</template>

<script>
  export default {
    data() {
      return {
        form: {
          email: '',
          password: ''
        },
        foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        show: true
      }
    },
    methods: {
    /** Previous activity*/
    /**register(){
     * console.log(this.form.email);
      *  console.log(this.form.password);
    },*/
    
      // Current activity
      //Step 3//
      register(){
      axios.post('/register/registration',this.form).then(response=>{
        console.log(response.data.email);
        console.log(response.data.password);
      }).catch(error=>{
        console.log(error.data);
        this.loading = false;
      })
      //Step 3//
      },

      //Regardless if this method is commented out, it will still outputs the desired outcome 
      onSubmit(event) {
        console.log(this.form.email);
        console.log(this.form.password);
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = ''
        this.form.food = null
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>