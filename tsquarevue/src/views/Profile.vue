<template>
	<NavBar/>
	<div v-if="isLoading" style="margin-top: 25%; height: 300px">
		<ui-spinner active></ui-spinner>
	</div>
	<div v-else-if="hasProfile" style="margin-top: 100px; height: 700px">
		<ProfileDisplay/>
	</div>
	<div v-else-if="myProfile" style="margin-top: 20%; height: 400px">
		<!-- <img class="animated-gif" src="@/assets/cute-sad.gif" alt=""> -->
		<h4>It seems like you have no tutor profile yet. <br><br> <a href="/createprofile">Click here to create your tutor profile now!</a></h4>
		<br>
	</div>
	<div v-else style="margin-top: 25%; height: 300px">
		<h4>This profile does not exist. Please try again.</h4>
	</div>
    <Footer/>
</template>

<script>

import NavBar from '../components/NavBar.vue'
import Footer from '../components/Footer.vue'
import ProfileDisplay from '../components/ProfileDisplay.vue'
import firebaseApp from '../firebase.js';
import { getFirestore, doc, getDoc } from "firebase/firestore"
import { getAuth } from "firebase/auth";
import { FirebaseError } from '@firebase/util';

const db = getFirestore(firebaseApp);

export default {
	name: "Profile",

	components: {
		NavBar,
		Footer,
		ProfileDisplay
	},

	data() {
		return {
			fbuser: "",
			hasProfile: false,
			myProfile: false,
			isLoading: true
		}
	},

	mounted() {
		const auth = getAuth(); 
		this.checkProfile();
	},

	methods: {
		async checkProfile() {
			setTimeout(() => {
				this.isLoading = false;
			}, 2000);
			const username = this.$route.params.username
			let docs = await getDoc(doc(db, "profiles", username))
			const current = getAuth().currentUser.email
			const currentUsername = String(current).split("@")[0]

			if (docs.exists()) {
				this.hasProfile = true;
			} else if (username.valueOf() == currentUsername.valueOf()) {
				this.myProfile = true;
			} else {
				console.log("Profile does not exist")
			}
		}
	}
}

	
</script>

<style scoped>
img.animated-gif{
  width: 200px;
  height: auto;
  
}


#bg { 
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 60%;
}

/* Footer {
	position: absolute;
	bottom:0;
	left:0;
	width:100%;
	height:300px;
} */

</style>