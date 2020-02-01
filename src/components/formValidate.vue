<template>
  <div class="container">
    <div class="row">
        <div class="col-md-8 offset-md-2">

              <form id="form">

                <div class="form-row">
                  <div class="col-md-4 mb-3 md-form">

                    <label for="validationServer015">First name</label>

                    <input type="text" v-model.trim="$v.name.$model" @input="setName($event.target.value)" class="form-control" :class="getClass()" name="name" id="validationServer015" value="Mark" autofocus>

                    <div class="invalid-feedback" v-if="!$v.name.required">
                      field is required
                    </div>

                    <div class="error" v-if="!$v.name.minLength">
                      Name must have at least {{$v.name.$params.minLength.min}} letters.
                    </div>

                  </div>

                  <div class="col-md-4 mb-3 md-form">

                    <label for="validationServerUsername55">Username</label>

                    <input type="text" v-model="$v.username.$model" :class="getUsername()" @input="setUsername($event.target.value)" class="form-control" name="username" id="validationServerUsername55">

                    <div class="invalid-feedback" v-if="!$v.username.required">
                      Please choose a username.
                    </div>

                    <div class="error" v-if="!$v.username.minLength">
                      Name must have at least {{$v.username.$params.minLength.min}} letters.
                    </div>

                  </div>


                  <div class="col-md-4 mb-3 md-form">

                    <label for="validationServerEmail55">Email</label>

                    <input type="email" class="form-control" :class="getEmail()" v-model.trim="$v.email.$model" @input="setEmail($event.target.value)" name="email" id="validationServerEmail55">

                    <div class="invalid-feedback" v-if="!$v.email.required">
                      Email is required
                    </div>

                    <div class="errorLength" v-if="!$v.email.minLength">
                      Name must have at least {{$v.email.$params.minLength.min}} letters.
                    </div>


                    <div class="error" v-if="!$v.email.email">
                      invalid Email
                    </div>

                  </div>

                </div>

                <button class="btn btn-primary btn-sm btn-rounded" type="submit" @click.prevent="post">Submit form</button>
          </form>

        </div>
    </div>


  </div>
</template>

<script type="text/javascript">
import { required, minLength, email } from 'vuelidate/lib/validators'

export default{
  name:'formValidate',
  // name
  data(){
    return{
      name: '',
      username: '',
      email: '',
      isValid: '',
    }
  },
  // data

  // computed

  validations:{
    name:{
      required,
      minLength: minLength(4)
    },
    // name
    username:{
      required,
      minLength: minLength(4)
    },
    // username
    email:{
      required,
      email,
      minLength: minLength(4)
    },
    // email
  },
  // validations

  methods:{
    setName(value){
      this.name = value
      this.$v.name.$touch()
    },
    setUsername(value){
      this.username = value
      this.$v.username.$touch()
    },
    setEmail(value){
      this.email = value
      this.$v.email.$touch()
    },

    getClass(){
      if (!this.$v.name.required) {
        return this.isValid = 'is-invalid'
      }

      else if(this.$v.name.minLength){
        return this.isValid = 'is-valid'
      }

      else{
        return this.isValid = 'is-invalid'
      }
    },

    getUsername(){
      if (!this.$v.username.required) {
        return this.isValid = 'is-invalid'
      }
      else if(this.$v.username.minLength)
      {
        return this.isValid = 'is-valid'
      }
      else{
        return this.isValid = 'is-invalid'
      }
    },
    // setName

    getEmail(){
      if (!this.$v.email.required) {
        return this.isValid = 'is-invalid'
      }
      else if(!this.$v.email.minLength)
      {
        return this.isValid = 'is-invalid'
      }
      else if(!this.$v.email.email)
      {
        return this.isValid = 'is-invalid'
      }
      else{
        return this.isValid = 'is-valid'
      }
    },
    // getEmail

    post(){


      const postData = {name: this.name, username: this.username, email: this.email};

      if (this.$v.$invalid) {
        alert('Submission Invalid');
      }else{

        this.$http.post('https://laravel-6ae0a.firebaseio.com/post.json', postData).then(res =>{

            this.data = res.body;

        });

        alert(this.name + ' '+ 'Just Submitted The form');

        this.name = this.email = this.username = '';

      }

    }

    // post
  },

  // END
}

</script>

<style media="screen" scoped>
.error{
    width: 100%;
    margin-top: .25rem;
    font-size: 80%;
    color: #dc3545;
}
.errorLength{
    width: 100%;
    margin-top: .25rem;
    font-size: 80%;
    color: #dc3545;
}
</style>
