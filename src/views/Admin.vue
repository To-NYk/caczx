<template>

        <div class="container mt-3">
            <div class="row">
                <div class="col-md-3"></div>
                <div class="col-md-6">
                    <form @submit.prevent="submit">
                        <div class="form-group my-2">
                            <input type="username" class="form-control" id="username" v-model="username" required
                                placeholder="Имя пользователя">
                        </div>
                        <div class="form-group my-2">
                            <input type="password" class="form-control" id="password" v-model="password" required
                                placeholder="Пароль">
                        </div>
                        <button @click="login" type="submit" class="btn btn-primary mt-3">Войти</button>
                    </form>
                </div>
                <div class="col-md-3"></div>
            </div>
        </div>
</template>

<script>
import axios from "axios"

export default {
    name: "LogInAdmin",
    data() {
        return {
            username: '',
            password: '',
            error: ''
        }

    },
    methods: {
        async login ()
        {
            let result = await axios.get(`http://localhost:9000/user?username=${this.username}&password=${this.password}`);
            console.warn(result);

            if(result.status==200 && result.data.length > 0)
            {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push('/')
            }
        } 
    }
}
</script>

<style lang="scss" scoped>

</style>