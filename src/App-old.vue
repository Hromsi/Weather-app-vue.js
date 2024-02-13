<template>
    <input type="text" v-model="userName" placeholder="Name"/>
    <input type="password" v-model="userPass" placeholder="password"/>
    <input type="email" v-model="userEmail" placeholder="email"/>
    <button @click="sendData()">Send</button>
    <p className="error">{{ error }}</p>
    <div v-if="users.length == 0" className="user">
        У нас нет Пользователей
    </div>
    <div v-else-if="users.length == 1" className="user">
        Users has 1 element
    </div>
    <div v-else className="user">
        Users has more than 1 element
    </div>

    <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser"/>
</template>

<script>
import User from './components/User.vue'

export default {
    components: { User },
    data() {
        return {
            error: '',
            users: [],
            userName: '',
            userPass: '',
            userEmail: '',
        }
    },
    methods: {
        sendData() {
            if(this.userName == '') {
                this.error = 'Имя не введено';
                return;
            } else if(this.userPass == '') {
                this.error = 'Пароль не введен';
                return;
            } else if(this.userEmail == '') {
                this.error = 'Email не введен';
                return;
            }
            this.error = '';
            this.users.push({
                name: this.userName,
                pass: this.userPass,
                email: this.userEmail,
            })
        },
        deleteUser(index) {
            this.users.splice(index, 1);
        }
    }
}
</script>

<style scoped>
.user {
    width: 500px;
    margin-top: 20px;
    border: 1px solid silver;
    background: #e3e3e3;
    color: #222;
    padding: 20px;
    border-radius: 5px;
}
</style>
