<template>   
    <div class="logIn_user">
    <div class="titulo">    
        <h1 style="font-size: 90px;position: relative;right: 604px;bottom: 405px;">Twezor.io</h1>
    </div>
        <div class="container_logIn_user">
            <form v-on:submit.prevent="processLogInUser" >
                <input type="text" v-model="user.username" placeholder="Username">
                <br>
                <input type="password" v-model="user.password" placeholder="Password">
                <br>
                <h2 style="font-size: 15px;">Forgot-your-password?</h2>
                <div class="link">
                <router-link class="link1" to="/user/signUp">Login</router-link>
                </div>
                <!--<p class="Forgot-your-password? text-right">
                    router link-->
                <h2 style="font-size: 15px;">Don't have an account? Sign Up?</h2>
            </form>
        </div>    
    </div>
    
</template>

<script>
import axios from 'axios';
            
export default {
    name: "LogIn",

    data: function(){
        return {
            user: {
                username:"",
                password:""
            }
        }
    },
    methods: {
        processLogInUser: function(){
            axios.post(
                "https://mision-tic-bank-be.herokuapp.com/login/",
                this.user,
                {headers: {}}
                )
                .then((result) => {
                    let dataLogIn = {
                    username: this.user.username,
                    token_access: result.data.access,
                    token_refresh: result.data.refresh,
                    }

                    this.$emit('completedLogIn', dataLogIn)
                })
                .catch((error) => {
                    if (error.response.status == "401")
                        alert("ERROR 401: Credenciales Incorrectas.");
                });
        }
    }
}
</script>

<style>
    .logIn_user{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        display: flex;
        justify-content: right;
        align-items: center;
    }
    .logIn_user h2{
        color:#f4f5f5;   
    }
    .titulo {
        margin-left: 15%;
        margin-top:40%;
    }
    
    h2{
        font-family: Arial, Helvetica, sans-serif;
        padding: 2%;
        text-align: center;
        font-weight: 100;
    }
    .container_logIn_user {    
        border-radius: 10px;
        width: 25%;
        height: 60%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .link{
        background-color: #2837478a;
        text-decoration: underline;
        font-size: 20px;
        padding: 8px;
        border-radius: 5px;
        
    }
    
    .logIn_user form{
        width: 95%;
        height: 90%;
        margin-right:65%;
    }

    .logIn_user input{
        height: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 10px 29px;
        margin: 11px 3px;
        border: 1px solid #283747;
        border-radius: 13px;
        align-content: right;
    }

    .logIn_user button{
        width: 100%;
        height: 40px;
        color: #E5E7E9;
        background: #283747;
        border: 1px solid #E5E7E9;
        border-radius: 19px;
        padding: 10px 25px;
        margin: 5px 0;
    }

    .logIn_user button:hover{
        color: #E5E7E9;
        background: crimson;
        border: 1px solid #283747;
    }
</style>