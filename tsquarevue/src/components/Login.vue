<template>
	<div class="container">
		<div class="mt-5 mb-5 topdiv" style="text-align:center;">    
            <img src="../assets/HomePage/LogoWhite.png" style="max-height: 350px; max-width: 350px;"> 
		</div>
        <div id="firebaseui-auth-container"></div>

        <div class="about mt-5">
            <div data-aos="fade-in">
                <h1 data-aos="fade-in">Our Mission</h1>
                <p>To make learning affordable and accessible to everyone.</p>
            </div>

            <div data-aos="fade-left">
                <h1>Our Motivation</h1>
                <p>T Square's users can play dual roles in tutoring other users and seeking tutoring services in other skills. We want to create a community of users who can learn new skills from one another. Our primary objective is to allow users to seek tutoring services from one another at no commission rate.</p>
            </div>

            <div data-aos="fade-right">
                <h1>Our Team</h1>
                <p>Our team consists of dedicated members from all walks of life, who work continuously to build this platform and grow our community of users</p>
            </div>
        </div>
        <BackToTop/>
	</div>
</template>

<script>
import BackToTop from './BackToTop.vue'
import firebase from '../uifire.js'
import 'firebase/compat/auth';
import * as firebaseui from 'firebaseui'
import 'firebaseui/dist/firebaseui.css'

export default {

    name: "Login",
	
	components: {
        BackToTop
	},

    mounted() {
        var ui = firebaseui.auth.AuthUI.getInstance();
        if (!ui) {
            ui = new firebaseui.auth.AuthUI(firebase.auth()); // Initialize the FirebaseUI Widget using Firebase
        }

        var uiConfig = {
            signInSuccessUrl: '/home',
            signInOptions: [
            firebase.auth.GoogleAuthProvider.PROVIDER_ID,
            firebase.auth.EmailAuthProvider.PROVIDER_ID,
            ]          
        };

        ui.start("#firebaseui-auth-container", uiConfig)
    }

}
</script>


<style scoped>

#firebaseui-auth-container{
	margin-top: 50px;;
	margin-bottom: 30px;;
}

#mainHead{
    text-align: center;
    text-shadow: 2px 2px grey;

}

/* Footer {
	position: absolute;
	bottom:0;
	left:0;
	width:100%;
	height:300px;
} */


</style>
