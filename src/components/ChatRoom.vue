<template>
    <div class="chat-window">
        <div class="messages">
            <div class="message"  v-for="messege in messeges" v-bind:key="messege._id">
                <div class="username"> {{messege.username}} </div>
                <div class="message-text"> {{messege.msg}} </div>
                 <div class="message-data"> {{messege.date}} </div>
            </div>

        </div>
        <form action="" class="imput-container" v-on:submit="sendMessege">
            <input type="text" v-model="msg"  class="form-control form-control-lg" placeholder="escriba mesnasje">
            <button v-on:click="sendMessege" v-bind:disabled="!msg"  class="btn btn-primary">send</button>
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
<style lang="scss" scoped>
.chat-window {
	flex: 1;
	display: flex;
	flex-direction: column;
	background-color: #F9F9F9;
	box-shadow: 1px 1px 6px 0px rgba(0, 0, 0, 0.15);
	.messages {
		flex: 1;
		overflow: scroll;
		.message {
			display: flex;
			border-bottom: 1px solid #EFEFEF;
			padding: 10px;
			&:last-of-type {
				border-bottom: none;
			}
			.username {
				width: 100px;
				margin-right: 15px;
			}
			.message-text {
					width: 100px;
				margin-right: 15px;
			}
			.message-data{
				flex: 1;
			}
		}
	}
	.input-container {
		display: flex;
		input {
			flex: 1;
			height: 35px;
			font-size: 18px;
			box-sizing: border-box;
		}
		button {
			width: 75px;
			height: 35px;
			box-sizing: border-box;
		}
	}
}
</style>