<template>
    <div class="box-holder dot_bg">
        <!--h1>Hi {{account.user.firstName}}!</h1-->
        <h5 class="mb-4 text-primary">You're logged in !!</h5>

        <p><b>Email :</b> {{user.data.attributes.email}} </p>
       
        <p>
            <router-link to="/login">Logout</router-link>
            <router-link to="/change-password" class="ml-4">Update Password</router-link>
        </p>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    computed: {
        ...mapState({
            user: state => state.users.user
        })
    },
    created () {
        this.getUserDetail();
    },
    methods: {
        ...mapActions('users', {
            getUserDetail: 'getUserDetail',
           // deleteUser: 'delete'
        })
    }
};
</script>
