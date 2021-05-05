<template>
<div>
    <div class="sidenav">
        <div class="login-main-text">
        <h2>Bienvenido<br> Página de registro</h2>
        <p>Ingresa tus datos para quedar registrado en nuestra base</p>
        </div>
    </div>
    <div class="main">
        <div class="col-md-6 col-sm-12">
        <div class="login-form">
            <form @submit.prevent="registro"> 
                <div class="form-group">
                    <label>E-mail</label>
                    <input type="email" class="form-control" placeholder="Ingrese E-mail" id="email">
                </div>
                <div class="form-group">
                    <label>Password</label>
                    <input type="password" class="form-control" placeholder="Password" id="password" >
                </div>
                <button type="submit" class="btn btn-secondary">Registrar Usuario</button>
            </form>
        </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'login',
    
    methods: {
                registro(){
                    var correo = document.getElementById('email').value;
                    var password = document.getElementById('password').value;

                    // console.log(correo);
                    // console.log(password);

                     firebase.auth().createUserWithEmailAndPassword(correo, password)
                        .then((userCredential) => {
                            // Signed in
                             var user = userCredential.user;
                             // ...
                        })
                        .catch((error) => {
                             var errorCode = error.code;
                            var errorMessage = error.message;
                            });
                        if (correo == "" | password ==""){
                            Swal.fire({
                            icon: 'error',
                            title: 'ups!!',
                            text: 'Debes llenar los campos :('
                            })
                        } else {
                            Swal.fire(
                            'Bienvenido!',
                            'Tu registro fue exitoso',
                            'success'
                            )

                        }
                    }
    }
};


</script>

<style>

* {
    font-family: "Lato", sans-serif;
}



.main-head{
    height: 150px;
    background: #FFF;
   
}


.sidenav {
    height: 100%;
    background-color: #000;
    overflow-x: hidden;
    padding-top: 20px;
}


.main {
    padding: 0px 100px;
   
}

@media screen and (max-height: 450px) {
    .sidenav {padding-top: 15px;}
}

@media screen and (max-width: 450px) {
    .login-form{
        margin-top: 10%;
    }

    .register-form{
        margin-top: 10%;
    }
}

@media screen and (min-width: 768px){
    .main{
        margin-left: 40%; 
    }

    .sidenav{
        width: 40%;
        position: fixed;
        z-index: 1;
        top: 0;
        left: 0;
    }

    .login-form{
        margin-top: 50%;
        margin-left: 40%;
    }

    .register-form{
        margin-top: 20%;
    }
}


.login-main-text{
    margin-top: 20%;
    padding: 60px;
    color: #fff;
}

label{
    color: #fff;
}

.login-main-text h2{
    font-weight: 300;
}

.btn-secondary{
    background-color: #000 !important;
    color: #fff;
    border: 2px solid;
    margin-top: 5px;
}

</style>


