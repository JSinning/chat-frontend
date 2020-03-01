<template>
    <div class="chat-window">
        <div class="messege">
            <div class="messege"  v-for="messege in messeges" v-bind:key="messege._id">
                <div class="username"> {{messege.username}} </div>
                <div class="messege-text"> {{messege.msg}} </div>
                 <div class="messege-text"> {{messege.date}} </div>
            </div>

        </div>
        <form action="" class="imput-container" v-on:submit="sendMessege">
            <input type="text" v-model="msg">
            <button v-on:click="sendMessege" v-bind:disabled="!msg">send</button>
        </form>
    </div>
</template>

<script>
export default {
    name:'chatRoom',
    props:['messeges'],
    data(){
        return{
            msg: ""
        }
    },
    methods:{
        sendMessege(){
            if (!this.msg) {
                alert('profavo dijiteun mesaje');
                return;
            }
            this.$emit('sendMessege', this.msg);
            this.msg = "";
        }
    }
}
</script>