<template>
    <div>
        <h2>Авторизация</h2>
        <form @submit.prevent="handleSubmit">
            <div class="form-group">
                <label for="username">Логин</label>
                <input type="text" v-model="username" name="username" class="form-control" :class="{ 'is-invalid': submitted && !username }" />
                <div v-show="submitted && !username" class="invalid-feedback">Введите логин</div>
            </div>
            <div class="form-group">
                <label htmlFor="password">Пароль</label>
                <input type="password" v-model="password" name="password" class="form-control" :class="{ 'is-invalid': submitted && !password }" />
                <div v-show="submitted && !password" class="invalid-feedback">Введите пароль</div>
            </div>
            <div class="form-group">
                <button class="btn btn-primary" :disabled="status.loggingIn">Вход</button>
                <span>Еще нет аккаунта? <router-link to="/register" class="btn btn-link">Зарегистрироваться</router-link></span>
            </div>
        </form>
    </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
    data () {
        return {
            username: '',
            password: '',
            submitted: false
        }
    },
    computed: {
        ...mapState('account', ['status'])
    },
    created () {
        // reset login status
        this.logout();
    },
    methods: {
        ...mapActions('account', ['login', 'logout']),
        handleSubmit (e) {
            this.submitted = true;
            const { username, password } = this;
            if (username && password) {
                this.login({ username, password })
            }
        }
    }
};
</script>