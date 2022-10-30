<template>
    <div class="home">
        <div class="homeLeft">
            <div class="titulo">
                <img id="logo" src="../../imagens/logoRotas-removebg-preview.png" alt="rotas">
                <h1>GERENCIADOR DE ROTAS</h1>

            </div>

            <img id="mapa" class="figuras" src="../../imagens/mapa.png" alt="Mapa">
            <img id="logoIfood" class="figuras" src="../../imagens/ifood.png" alt="Ifood">
        </div>

        <div class="homeRight">

            
            <h1 id="titleRight">{{modo.titulo}}</h1>
           

            <div class="form">
              
                
                <div class="input">
                     <div class="iconEmail"></div>
                     <input  type="email" placeholder="E-mail" v-model="email"/>        
                </div>

                        <div class="subForm" v-show="campoInvalido.email">
                            <span class="alertForm">* Campo obrigatório</span>
                        </div>



                <Transition name="fade"> 
                    <div class="input" v-show="modo.titulo == 'REGISTRE-SE'">
                        <div class="iconUsuario"></div>
                        <input  type="text" placeholder="Usuário" v-model="usuario"/> 
                    </div>
                </Transition> 

                        <div class="subForm" v-show="campoInvalido.usuario && modo.titulo == 'REGISTRE-SE'" >
                                <span class="alertForm">* Campo obrigatório</span>
                        </div>


                      
                <div class="input">
                    <div class="iconSenha"></div>
                    <input  type="password" placeholder="Senha" v-model="senha"/> 
                </div>

                        <div class="subForm" v-show="campoInvalido.senha">
                            <span class="alertForm">* Campo obrigatório</span>
                        </div>



                <Transition name="fade">
                    <div class="input" v-show="confirmarSenha && modo.titulo == 'REGISTRE-SE'">
                        <div class="iconSenha"></div>
                        <input  type="password" placeholder="Confirme a Senha" v-model="confSenha"/> 
                    </div>
                </Transition>    

                        <div class="subForm" v-show="campoInvalido.confSenha && confirmarSenha && modo.titulo == 'REGISTRE-SE'">
                            <span class="alertForm">* Campo obrigatório</span>
                        </div>
                        <div class="subForm" v-show="confirmarSenha">
                            <span class="alertForm">{{msgConfirmarSenha}}</span>
                        </div>
                       
                
                <AppBtnSubmit :nome="modo.nomeSubmit" @click.native="submit(modo.titulo)" />

                       
            </div>

            <div class="footer">
                    <span>Você já é cadastrado?</span>
                   <AppBtnMode @click.native="pagLogin()" :nome="modo.btnAlteraModo"/>
                   
                </div> 
           
        </div>

    </div>
</template>

<script>
import AppBtnSubmit from '../btnSubmit/AppBtnSubmit.vue'
import AppBtnMode from '../btnModo/AppBtnModo.vue'

export default {
    components:{ AppBtnSubmit, AppBtnMode },
data(){
    return{
        email: '',
        usuario:'',
        senha:'',
        confSenha: '',
        modo: {
            titulo: 'REGISTRE-SE',
            nomeSubmit: 'CADASTRAR',
            btnAlteraModo: 'Login'
        },
        campoInvalido: {
            email: false,
            usuario: false,
            senha: false,
            confSenha: false,
            
        } 
    }
},
methods:{
    pagLogin(){
        if(this.modo.titulo === 'REGISTRE-SE'){

            this.modo.titulo = 'LOGIN'
            this.modo.nomeSubmit = 'ENTRAR'
            this.modo.btnAlteraModo = 'Registre-se'
        } else {
            this.modo.titulo = 'REGISTRE-SE'
            this.modo.nomeSubmit = 'CADASTRAR'
            this.modo.btnAlteraModo = 'Login'
        }
        this.campoInvalido.email = false
        this.campoInvalido.usuario = false
        this.campoInvalido.senha = false
        this.campoInvalido.confSenha = false
       
    },

    validacaoForm(){
        if(this.email == ''){
            this.campoInvalido.email = true
        } else {
            this.campoInvalido.email = false
        }
        if(this.usuario == ''){
            this.campoInvalido.usuario = true
        } else {
            this.campoInvalido.usuario = false
        }
        if(this.senha == ''){
            this.campoInvalido.senha = true
        } else {
            this.campoInvalido.senha = false
        }
        if(this.confSenha == ''){
            this.campoInvalido.confSenha = true
        } else {
            this.campoInvalido.confSenha = false
        }
    },

    submit(params){
        
        this.validacaoForm()

        if(params == 'REGISTRE-SE' && !this.campoInvalido.email
             && !this.campoInvalido.usuario 
             && !this.campoInvalido.senha 
             && !this.campoInvalido.confSenha){
              this.registro()
             
        } else{
            this.login()    
        }
    },

    registro(){
        let myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/json");

        let raw = JSON.stringify({
        "email": this.email,
        "username": this.usuario,
        "password": this.confSenha
        });

        let requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
        };

        fetch("http://191.252.193.209:3333/users", requestOptions)
            .then(response => response.text())
            .then(result => console.log(result))
            .catch(error => console.log('error', error));
        },

    login(){
        var myHeaders = new Headers();
        myHeaders.append("Content-Type", "application/json");

        var raw = JSON.stringify({
        "email": this.email,
        "password": this.senha
        });

        var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
        };

        fetch("http://191.252.193.209:3333/sessions", requestOptions)
            .then(response => response.text())
            .then(result => console.log(result))
            .catch(error => console.log('error', error));
    }

},
computed:{
    confirmarSenha(){
        let resultado
        if(this.senha == ''){
            resultado = false
        } else {
            resultado = true
        }
        return resultado
    },
    msgConfirmarSenha(){
        let resultado
        if(this.confSenha != this.senha && this.confSenha != ''){
            resultado = 'As senhas não são iguais'
        }
        return resultado
    }
},
watch:{
    email(){
        if(this.email != ' '){
            this.campoInvalido.email = false
        }
    },
    usuario(){
        if(this.usuario != ' '){
            this.campoInvalido.usuario = false
        }
    },
    senha(){
        if(this.senha != ' '){
            this.campoInvalido.senha = false
        }
    },
   confSenha(){
    if(this.confSenha != ' '){
        this.campoInvalido.confSenha = false
    }
   }
}
}
</script>

<style src="./style.scss" lang="scss" scoped />

