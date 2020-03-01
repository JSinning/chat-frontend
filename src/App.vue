<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>chat</h1>
    <p class="username"> username:  {{username}} </p>
    <p class="onlie"> onlie: {{users.length}} </p>
    <chatRoom v-bind:messeges="messeger" v-on:sendMessege="this.sendMessege"/>
  </div>
</template>

<script>
import io from "socket.io-client";
import ChatRoom from './components/ChatRoom';
export default {
  name: 'App',
  components:{
    ChatRoom
  },
  data(){
    return {
      username: "",
      stocke: io("http://localhost:3000/"),
      messeger:[],
      users:[],
    }
  },
  methods:{
    joinServe(){
      this.stocke.on('loggedIn', data =>{
        this.messeger = data.mensaje;
        this.users =  data.users;
        this.stocke.emit('newuser', this.username);
        console.log(this.users);
        console.log(this.messeger);

      });

      this.lisenet();

    },
    lisenet(){
      this.stocke.on('useronline', user =>{
        this.users.push(user);
      });
      this.stocke.on('userLef', user =>{
        this.users.splice(this.users.indexOf(user), 1);

      })
      this.stocke.on('msg', messege =>{
        this.messeger.push(messege)
      });
    },
    sendMessege(messege){
      this.stocke.emit('msg', messege);
    }

  },
  mounted:function(){
    this.username = prompt("¿cual es tu usuario?, anonimuys");
    if (!this.username) {
      this.username = "anomymus";
    
    }
    this.joinServe();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
