<template>
    <div>
        <!--h1>Hi {{account.user.firstName}}!</h1-->
        <p>You're logged in !!</p>

        <p><b>Email :</b> {{user.data.attributes.email}} </p>
       
        <p>
            <router-link to="/login">Logout</router-link>
            <router-link to="/change/password" class="ml-4">Change Password</router-link>
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
