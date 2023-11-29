<template>
    <div class="col-4">
        <div class="card">
            <div class="card-body">
                <h5 class="card-title mb-4">Sign In</h5>

                <el-form ref="form" :model="form" :rules="rulesForm">
                <p v-if="Object.keys(validationErrors).length != 0" class='text-center '><small class='text-danger'>Incorrect Email or Password</small></p>
                <el-form-item label="Email" prop="email">
                    <el-input v-model="form.email" prop="email"></el-input>
                </el-form-item>
                <el-form-item label="Password" prop="password">
                    <el-input show-password v-model="form.password" prop="password"></el-input>
                </el-form-item>
                    
                <div class="d-grid gap-2">
                    <el-button 
                        :disabled="isSubmitting"
                        @click="loginAction('form')"
                        type="primary">Login
                    </el-button>
                    <p class="text-center">Ya tienes una cuenta? 
                        <el-link type="primary" href="/register">Click aqui</el-link>
                    </p>
                </div>
            </el-form>
            
            </div>
        </div>
    </div>
 </template>
   
<script>
   
 export default {
   name: 'LoginPage',
   data() {
     return {
        form:{
            email:'',
            password:'',
        },
        rulesForm:{
            email:[{required: true, message: 'El email no puede estar vacio', trigger: 'blur'}],
            password:[{required: true, message: 'La password no puede ser vacia', trigger: 'blur'}],
        },
        
        validationErrors:{},
        isSubmitting:false,
     };
   },
   methods: {
      loginAction(form){
        this.$refs[form].validate((valid) => {
            
            if(valid){
                var form = this.form;
                this.isSubmitting = true
                axios.post('/login/loguearse', form)
                .then(response => {

                    localStorage.setItem('token', response.data.token)
                })
                .catch({
                    
                });
            }
        });
      }
   },
 };
</script>
