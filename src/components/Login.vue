<template>
<div class='login'>
<div class="limiter">
		<div class="container-login100">
			<div class="wrap-login100">
				<form class="login100-form validate-form">
					<span class="login100-form-title p-b-26">
						Welcome!
					</span>
					<span class="login100-form-title p-b-48">
						<i class="zmdi zmdi-font"></i>
					</span>

					<div class="wrap-input100 validate-input" data-validate = "Valid email is: a@b.c">
						<input class="input100" type="text" name="email" placeholder="Email" v-model='email'>
						<span class="focus-input100" data-placeholder="Email"></span>
					</div>

					<div class="wrap-input100 validate-input" data-validate="Enter password">
						<input class="input100" :type="type" name="pass" placeholder="Password" v-model='password'>
						<span class="focus-input100" data-placeholder="Password"></span>
                        <span class="btn-show-pass">
							<img class="visible-eye" src="./../assets/visibility.png" v-if="!passwordVisible" v-on:click="togglePasswordVisibility">
                            <img class="invisible-eye" src="./../assets/invisible.png" v-if="passwordVisible" v-on:click="togglePasswordVisibility">
						</span>
					</div>

					<div class="container-login100-form-btn">
						<div class="wrap-login100-form-btn">
							<div class="login100-form-bgbtn"></div>
							<button class="login100-form-btn" v-on:click="login">
								Login
							</button>
						</div>
					</div>
					<div v-if='error'><p class='alert'>{{this.errorMessage}}</p></div>

					<div class="text-center p-t-75">
						<span class="txt1">
							Don’t have an account?
						</span>

						<router-link class="txt2" to=/register exact>
							<span class='txt2'>Register</span>
						</router-link>
					</div>
				</form>
			</div>
		</div>
	</div>
    </div>
</template>


<script>
import firebase from 'firebase';
    

export default {
    
    data() {
        return {
            email: '',
            psasword: '',
            passwordVisible: false,
            eyeIconVisible: false,
            type: "password",
			error: false,
			errorMessage: 'Invalid email or password.'
        }
    },

    methods: {
        login: function(e){
            firebase.auth().signInWithEmailAndPassword(this.email, this.password)
            .then(user => {
                console.log(user)
                // alert(`You are logged in as ${user.user.email}`)
                this.$router.go({path: this.$router.path});
            },
            err => {
                console.log(err);
				this.error =true;
            });
            e.preventDefault();
        },

        togglePasswordVisibility() {
            this.eyeIconVisible = !this.eyeIconVisible
            this.passwordVisible = !this.passwordVisible
            if (this.type == "password") {
                this.type = "text"
            } else {
                this.type = "password"
            }
            
        }
    }
}

</script>


<style>
@import "./../css/util.css";
@import "./../css/main.css";

.button-show-pass {
    width: 100px;
}

.visible-eye,
.invisible-eye {
    width: 100%;
    overflow: hidden;
}

.input100::-webkit-input-placeholder { color: transparent;}
.input100:-moz-placeholder { color: transparent;}
.input100::-moz-placeholder { color: transparent;}
.input100:-ms-input-placeholder { color: transparent;}

.alert {
	margin-top: 10px;
	color: red;
}

router-link {
	color: #080808;
}

.txt2 {
	font-size: 13px;
	font-family: Poppins-Regular;
	color: #666666;
	text-decoration-color: #666666;
}

.container-login100 {
	background-image: url("./../assets/account-banner.jpeg");
	background-size: cover;
}

</style>


	