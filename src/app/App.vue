<template>
         <div class="h-100 d-flex align-items-center background-full">
        <div class="container">
            <div class="row">
                <div class="col-12">
                    <div v-if="alert.message" :class="`alert ${alert.type}`">{{alert.message}}</div>
                    <router-view></router-view>
                </div>
            </div>
        </div>
        </div>

</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    name: 'app',
    computed: {
        ...mapState({
            alert: state => state.alert
        })
    },
    methods: {
        ...mapActions({
            clearAlert: 'alert/clear' 
        })
    },
    watch: {
        $route (to, from){
            // clear alert on location change
            this.clearAlert();
        }
    } 
};
</script>

<style>
html, body {
	height: 100%;
}
body {
	padding-bottom: 53px;
}
.background-full {
	background-image: url(/src/assets/images/bg-1.jpg);
	background-size: cover;
	background-attachment: fixed;
	background-position: center;
}
.box-holder {
	max-width: 681px;
	margin-left: auto;
	margin-right: auto;
	box-shadow: 0px 14.095px 40px 8px rgba(0,0,0,0.35);
	padding: 50px;
	border-radius: 1rem;
	background-color: #fff;
}
.btn-primary {
	background-color: #0071BC;
	border: none;
	min-width: 100px;
	padding: 9px 15px;
}
.btn-primary:hover {
	background-color: #00BAFF;
}
.btn-link {
	color: #0071BC;
}
a{
	color: #0071BC;
}
.text-primary {
	color: #0071BC !important;
}
.box-holder.dot_bg{
	background-image: url(/src/assets/images/dot-grid.jpg);
    background-repeat: repeat;
}
.page-footer {
	box-shadow: 6px 6px 20px rgba(0,0,0,0.2);
}
.page-footer p {
	font-size: 14px;
}
.form-control {
	min-height: 43px;
}
.logo-icon img {
	max-width: 140px;
}
.form-title {
	font-weight: 700;
	margin-bottom: 20px;
}
.h1, .h2, .h3, .h4, .h5, .h6, h1, h2, h3, h4, h5, h6 {
	font-weight: 700;
}
.alert {
	max-width: 681px;
	margin-left: auto;
	margin-right: auto;
	padding: .35rem 1.25rem;
	font-size: 14px;
}
@media(max-width: 767px){
.box-holder {
	padding: 30px;
}
.form-title {
	font-size: 24px;
}
.logo-icon img {
	max-width: 110px;
}

}
</style>