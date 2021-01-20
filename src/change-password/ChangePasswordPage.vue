<template>
    <div class="box-holder dot_bg">
        <h2>Update Setting   <p>  </p></h2>
        <form @submit.prevent="handleSubmit">
            <div class="form-group">
                <label for="email">Email</label>
                <input type="email" v-model="user.email"  v-validate="'required'" name="email" class="form-control" :class="{ 'is-invalid': submitted && errors.has('email') }" />
                <div v-if="submitted && errors.has('email')" class="invalid-feedback">{{ errors.first('email') }}</div>
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" v-model="user.password" v-validate="'required'" name="password" class="form-control" :class="{ 'is-invalid': submitted && errors.has('password') }" />
                <div v-if="submitted && errors.has('password')" class="invalid-feedback">{{ errors.first('password') }}</div>
            </div>
            <div class="form-group">
                <label for="password_confirmation">Confirm Password</label>
                <input type="password" v-model="user.password_confirmation" v-validate="'required'" name="password_confirmation" class="form-control" :class="{ 'is-invalid': submitted && errors.has('password_confirmation') }" />
                <div v-if="submitted && errors.has('password_confirmation')" class="invalid-feedback">{{ errors.first('password_confirmation') }}</div>
            </div>
            <div class="form-group">
                <button class="btn btn-primary mr-2" :disabled="status.changePassword">Submit</button>
                <img v-show="status.changePassword" src="data:image/gif;base64,R0lGODlhEAAQAPIAAP///wAAAMLCwkJCQgAAAGJiYoKCgpKSkiH/C05FVFNDQVBFMi4wAwEAAAAh/hpDcmVhdGVkIHdpdGggYWpheGxvYWQuaW5mbwAh+QQJCgAAACwAAAAAEAAQAAADMwi63P4wyklrE2MIOggZnAdOmGYJRbExwroUmcG2LmDEwnHQLVsYOd2mBzkYDAdKa+dIAAAh+QQJCgAAACwAAAAAEAAQAAADNAi63P5OjCEgG4QMu7DmikRxQlFUYDEZIGBMRVsaqHwctXXf7WEYB4Ag1xjihkMZsiUkKhIAIfkECQoAAAAsAAAAABAAEAAAAzYIujIjK8pByJDMlFYvBoVjHA70GU7xSUJhmKtwHPAKzLO9HMaoKwJZ7Rf8AYPDDzKpZBqfvwQAIfkECQoAAAAsAAAAABAAEAAAAzMIumIlK8oyhpHsnFZfhYumCYUhDAQxRIdhHBGqRoKw0R8DYlJd8z0fMDgsGo/IpHI5TAAAIfkECQoAAAAsAAAAABAAEAAAAzIIunInK0rnZBTwGPNMgQwmdsNgXGJUlIWEuR5oWUIpz8pAEAMe6TwfwyYsGo/IpFKSAAAh+QQJCgAAACwAAAAAEAAQAAADMwi6IMKQORfjdOe82p4wGccc4CEuQradylesojEMBgsUc2G7sDX3lQGBMLAJibufbSlKAAAh+QQJCgAAACwAAAAAEAAQAAADMgi63P7wCRHZnFVdmgHu2nFwlWCI3WGc3TSWhUFGxTAUkGCbtgENBMJAEJsxgMLWzpEAACH5BAkKAAAALAAAAAAQABAAAAMyCLrc/jDKSatlQtScKdceCAjDII7HcQ4EMTCpyrCuUBjCYRgHVtqlAiB1YhiCnlsRkAAAOwAAAAAAAAAAAA==" />
                <router-link to="/" class="btn btn-link">Back</router-link>
            </div>
        </form>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    data () {
        return {
            user: {
                email: '',
                password: '',
                password_confirmation: '',
            },
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status']),

         ...mapState({
            userinfo: state => state.users.user
        })
    },
     created () {
        this.getUserDetail();
    },
    methods: {
        ...mapActions('account', ['changePassword']),
         ...mapActions('users', {
            getUserDetail: 'getUserDetail',
           // deleteUser: 'delete'
        }),
        handleSubmit(e) {
            this.submitted = true;
            this.$validator.validate().then(valid => {
                if (valid) {
                    console.log(this.user);
                    this.changePassword({user: this.user});
                }
            });
        }
    }
};
</script>
