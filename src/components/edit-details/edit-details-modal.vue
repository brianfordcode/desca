<template>

<div style="display: flex; align-items: center; justify-content: space-around;">
    <!-- PROFILE ICON AND LOG IN/OUT -->
    <div
        class="prof-img-container"
        v-if="profileDetails"
        @click= "$store.state.loggedIn ? openProfDetails() : logIn()"
        title="edit details"
    >
        <img
            class="profile-icon circle"
            :src="$store.state.loggedIn ? profileDetails.profPic.photoURL : '/profile-icon.png'"
            alt="prof-icon"
        >
        <div style="margin-left: 5px; color: white;">&#9660;</div>
        
    </div>

    <darkModeToggle style="margin-left:25px;"/>
</div>

    <!-- MODAL -->
    <div class="modal-container" v-if="editDetailsToggle">
        <div class="details-box-wrapper round-edges">
            <!-- BUTTONS -->
            <div
                class="discard-changes-btn btn bottom-left-btn"
                @click="discardChanges()"
                title="discard changes"
            >
            <img class="icon" src="../../assets/nav-icons/discard-icon.png" alt="remove-icon">
            </div>
            <div
                class="submit-btn bottom-right-btn btn"
                @click="submit()"
                title="submit"
            >
            <img class="icon" src="../../assets/nav-icons/submit-icon.png" alt="submit-icon">
            </div>
            <div
                class="logout-btn btn top-left-btn"
                @click="logOut()"
                title="log out"
            >
            <img class="icon" src="../../assets/nav-icons/logout-icon.png" alt="logout-btn">
            </div>

            <changeDetails :editProfileDetails="editProfileDetails" style="margin: 45px;"/>
        
        </div>
    </div>

</template>

<script>
import changeDetails from './details-change-box.vue'
import darkModeToggle from '../dark-mode-toggle.vue'

function copy(value) {
  return JSON.parse(JSON.stringify(value))
}

export default {
    data() {
        return {
            editProfileDetails: null,
            editDetailsToggle: false,
        }
    },
    components: { changeDetails, darkModeToggle },

    methods: {
        logIn() {
            this.$store.dispatch('logIn')
        },
        openProfDetails() {
            this.editProfileDetails = copy(this.profileDetails)
            this.editDetailsToggle = true
        },
        discardChanges() {

            const user = this.$store.state.user
            const profPicId = this.profileDetails.profPic.profPicId
            
            if (profPicId && profPicId != this.editProfileDetails.profPic.profPicId) { 
                this.$store.dispatch('deleteProfPic', {user, profPicId})
            }
            
            this.$store.dispatch('openActionModal', {text: 'changes discarded', color: 'red'})
            this.editDetailsToggle = false
        },
        submit() {

            const user = this.$store.state.user
            const profPicId = this.profileDetails.profPic.profPicId
            
            if (profPicId && profPicId != this.editProfileDetails.profPic.profPicId) { 
                this.$store.dispatch('deleteProfPic', {user, profPicId})
            }

            this.$store.dispatch('changeDetails', { details: this.editProfileDetails, user: this.$store.state.user.uid})
            this.$store.dispatch('openActionModal', {text: 'details changed', color: 'green'})

            this.editDetailsToggle = false
        },
        logOut() {
            this.editDetailsToggle = false
            this.$store.dispatch('logOut')
        }
    },
    computed: {
        profileDetails() {
            return this.$store.getters.getProfileDetails(this.$route.params.user)
        }
    }

}

</script>

<style scoped>
.modal-container {
    height: 100%;
    width: 100%;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    z-index: 999999999999999999;
    background-color: rgba(0,0,0,0.7);
    position: absolute;
    display: flex;
    justify-content: space-around;
    align-items: center;
    animation:  fadeIn .175s; 
}

.details-box-wrapper {
    background-color: white;
    position: relative;
    animation:  fadeIn .25s; 
}

.discard-changes-btn {
    background-color: rgb(182, 13, 13);
}

.submit-btn {
    background-color: rgb(11, 129, 25);
}

.logout-btn {
    background-color: rgb(41, 44, 236);
}
.prof-img-container {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-left: 10px;
}

.profile-icon {
    object-fit: cover;
    width: 30px;
    height: 30px;
}

@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}

</style>