<template>
    <div class="content">
        <div class="form sign-in">
            <h2>欢迎回来</h2>
            <el-form :model="param" :rules="rules" ref="login" label-width="0px" class="ms-content">
                <el-form-item prop="username">
                    <label>
                        <el-input v-model="param.username" type="text" placeholder="username">
                            <el-button class="elbtn" slot="prepend" icon="el-icon-lx-people"></el-button>
                        </el-input>
                    </label>
                </el-form-item>
                <el-form-item prop="password">
                    <label>
                        <el-input type="password" placeholder="password" v-model="param.password" @keyup.enter.native="submitForm()">
                            <el-button class="elbtn" slot="prepend" icon="el-icon-lx-lock"></el-button>
                        </el-input>
                    </label>
                </el-form-item>
            </el-form>
            <p class="forgot-pass"><a href="javascript:">忘记密码？</a></p>
            <button type="button" class="submit">登 录</button>
            <!--<button type="button" class="fb-btn">使用 <span>facebook</span> 帐号登录</button>-->
        </div>
        <div class="sub-cont">
            <div class="img">
                <div class="img__text m--up">
                    <h2>还未注册？</h2>
                    <p>立即注册，发现大量机会！</p>
                </div>
                <div class="img__text m--in">
                    <h2>已有帐号？</h2>
                    <p>有帐号就登录吧，好久不见了！</p>
                </div>
                <div class="img__btn">
                    <span class="m--up">注 册</span>
                    <span class="m--in">登 录</span>
                </div>
            </div>
            <div class="form sign-up">
                <h2>立即注册</h2>
                <el-form :model="param" :rules="rules" ref="register" label-width="0px" class="ms-content">
                    <el-form-item prop="phone">
                        <label>
                            <el-input v-model="param.phone" type="text" placeholder="请输入手机号"></el-input>
                        </label>
                    </el-form-item>
                    <el-form-item prop="veriCode">
                        <label>
                            <el-input v-model="param.veriCode" type="text" placeholder="请输入验证码" />
                        </label>
                    </el-form-item>
                </el-form>
                <el-button id="id-btn-get-code" style="background-color: #2d8cf0" onclick="clickBtn()">获取验证码</el-button>
                <button type="button" class="submit">注 册</button>
                <!--<button type="button" class="fb-btn">使用 <span>facebook</span> 帐号注册</button>-->
            </div>
        </div>
    </div>
</template>

<script>
    let btnRegTimer = null;
    export default {
        name: "Login",
        data: function() {
            return {
                param: {
                    username: '',
                    password: '',
                    phone: '',
                    veriCode: '',
                },
                rules: {
                    username: [{ required: true, message: '请输入用户名', trigger: 'blur' }],
                    password: [{ required: true, message: '请输入密码', trigger: 'blur' }],
                    phone: [{ required: true, message: '请输入手机号', trigger: 'blur' }],
                    veriCode: [{ required: true, message: '请输入验证码', trigger: 'blur' }],
                },
            };
        },
        methods: {
            submitForm() {
                this.$refs.login.validate(valid => {
                    if (valid) {
                        this.$message.success('登录成功');
                        localStorage.setItem('ms_username', this.param.username);
                        this.$router.push('/');
                    } else {
                        this.$message.error('请输入账号和密码');
                        console.log('error submit!!');
                        return false;
                    }
                });
            },
            clickBtn(){
                var v_btn=document.getElementById("id-btn-get-code");
                v_btn.disabled=true;
                v_btn.innerText="60s后可重新发送";
                window.clearInterval(btnRegTimer);
                var btnRegSec = 60;
                btnRegTimer = window.setInterval(function () {
                    if (btnRegSec==0){
                        v_btn.disabled=false;
                        v_btn.innerText="获取验证码";
                        window.clearInterval(btnRegTimer);
                    }else {
                        btnRegSec--;
                        v_btn.innerText=btnRegSec+"s后可重新发送";
                    }
                },1000)
            }
        },

    }
    window.onload=function(){
        document.querySelector('.img__btn').addEventListener('click', function() {
            document.querySelector('.content').classList.toggle('s--signup')
        })
    }

    /*window.onload=function () {
        var v_btn=document.getElementById("id-btn-get-code");
        v_btn.disabled=true;
        v_btn.innerText="60s后可重新发送";
        window.clearInterval(btnRegTimer);
        var btnRegSec = 60;
        btnRegTimer = window.setInterval(function () {
            if (btnRegSec==0){
                v_btn.disabled=false;
                v_btn.innerText="获取验证码";
                window.clearInterval(btnRegTimer);
            }else {
                btnRegSec--;
                v_btn.innerText=btnRegSec+"s后可重新发送";
            }
        },1000)
    }*/

    /*document.querySelector('.img__btn').addEventListener('click', function() {
        document.querySelector('.content').classList.toggle('s--signup')
    })*/
</script>

<style scoped>
    *, *:before, *:after {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    body {
        font-family: 'Open Sans', Helvetica, Arial, sans-serif;
        background: #ededed;
    }

    input, button {
        border: none;
        outline: none;
        background: none;
        font-family: 'Open Sans', Helvetica, Arial, sans-serif;
    }

    .tip {
        font-size: 20px;
        margin: 40px auto 50px;
        text-align: center;
    }

    .content {
        overflow: hidden;
        position: absolute;
        left: 50%;
        top: 50%;
        width: 900px;
        height: 550px;
        margin: -300px 0 0 -450px;
        background: #fff;
    }

    .form {
        position: relative;
        width: 640px;
        height: 100%;
        transition: -webkit-transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out, -webkit-transform 0.6s ease-in-out;
        padding: 50px 30px 0;
    }

    .sub-cont {
        overflow: hidden;
        position: absolute;
        left: 640px;
        top: 0;
        width: 900px;
        height: 100%;
        padding-left: 260px;
        background: #fff;
        transition: -webkit-transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out, -webkit-transform 0.6s ease-in-out;
    }

    .content.s--signup .sub-cont {
        -webkit-transform: translate3d(-640px, 0, 0);
        transform: translate3d(-640px, 0, 0);
    }

    button {
        display: block;
        margin: 0 auto;
        width: 260px;
        height: 36px;
        border-radius: 30px;
        color: #fff;
        font-size: 15px;
        cursor: pointer;
    }

    .img {
        overflow: hidden;
        z-index: 2;
        position: absolute;
        left: 0;
        top: 0;
        width: 260px;
        height: 100%;
        padding-top: 360px;
    }

    .img:before {
        content: '';
        position: absolute;
        right: 0;
        top: 0;
        width: 900px;
        height: 100%;
        background-image: url(src/assets/img/bg.jpg);
        background-size: cover;
        transition: -webkit-transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out, -webkit-transform 0.6s ease-in-out;
    }

    .img:after {
        content: '';
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.6);
    }

    .content.s--signup .img:before {
        -webkit-transform: translate3d(640px, 0, 0);
        transform: translate3d(640px, 0, 0);
    }

    .img__text {
        z-index: 2;
        position: absolute;
        left: 0;
        top: 50px;
        width: 100%;
        padding: 0 20px;
        text-align: center;
        color: #fff;
        transition: -webkit-transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out;
        transition: transform 0.6s ease-in-out, -webkit-transform 0.6s ease-in-out;
    }

    .img__text h2 {
        margin-bottom: 10px;
        font-weight: normal;
    }

    .img__text p {
        font-size: 14px;
        line-height: 1.5;
    }

    .content.s--signup .img__text.m--up {
        -webkit-transform: translateX(520px);
        transform: translateX(520px);
    }
    .img__text.m--in {
        -webkit-transform: translateX(-520px);
        transform: translateX(-520px);
    }

    .content.s--signup .img__text.m--in {
        -webkit-transform: translateX(0);
        transform: translateX(0);
    }

    .img__btn {
        overflow: hidden;
        z-index: 2;
        position: relative;
        width: 100px;
        height: 36px;
        margin: 0 auto;
        background: transparent;
        color: #fff;
        text-transform: uppercase;
        font-size: 15px;
        cursor: pointer;
    }
    .img__btn:after {
        content: '';
        z-index: 2;
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        border: 2px solid #fff;
        border-radius: 30px;
    }

    .img__btn span {
        position: absolute;
        left: 0;
        top: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        height: 100%;
        transition: -webkit-transform 0.6s;
        transition: transform 0.6s;
        transition: transform 0.6s, -webkit-transform 0.6s;
    }

    .img__btn span.m--in {
        -webkit-transform: translateY(-72px);
        transform: translateY(-72px);
    }

    .content.s--signup .img__btn span.m--in {
        -webkit-transform: translateY(0);
        transform: translateY(0);
    }

    .content.s--signup .img__btn span.m--up {
        -webkit-transform: translateY(72px);
        transform: translateY(72px);
    }

    h2 {
        width: 100%;
        font-size: 26px;
        text-align: center;
    }

    label {
        display: block;
        width: 260px;
        margin: 25px auto 0;
        text-align: center;
    }

    .elbtn{
        width: 3px;
    }

    label span {
        font-size: 12px;
        color: #909399;
        text-transform: uppercase;
    }

    input {
        display: block;
        width: 100%;
        margin-top: 5px;
        padding-bottom: 5px;
        font-size: 16px;
        border-bottom: 1px solid rgba(0, 0, 0, 0.4);
        text-align: center;
    }

    .forgot-pass {
        margin-top: 15px;
        text-align: center;
        font-size: 12px;
        color: #cfcfcf;
    }

    .forgot-pass a {
        color: #cfcfcf;
    }

    .submit {
        margin-top: 40px;
        margin-bottom: 20px;
        background: #d4af7a;
        text-transform: uppercase;
    }

    .fb-btn {
        border: 2px solid #d3dae9;
        color: #8fa1c7;
    }
    .fb-btn span {
        font-weight: bold;
        color: #455a81;
    }

    .sign-in {
        transition-timing-function: ease-out;
    }
    .content.s--signup .sign-in {
        transition-timing-function: ease-in-out;
        transition-duration: 0.6s;
        -webkit-transform: translate3d(640px, 0, 0);
        transform: translate3d(640px, 0, 0);
    }

    .sign-up {
        -webkit-transform: translate3d(-900px, 0, 0);
        transform: translate3d(-900px, 0, 0);
    }
    .content.s--signup .sign-up {
        -webkit-transform: translate3d(0, 0, 0);
        transform: translate3d(0, 0, 0);
    }

</style>

