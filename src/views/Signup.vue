<template>
    <div class="row my-5">
        <div class="col-md-6 offset-md-3">
            <div class="card">
                <div class="card-body">
                    <h3 class="text-center my-2">Register</h3>
                    <div class="form-group">
                        <input v-model="name" type="text" placeholder="Name" class="form-control">
                        <div class="errors" v-if="errors.name">
                            <small class="text-danger" :key="error" v-for="error in errors.name">{{error}}</small>
                        </div>
                    </div>
                    <div class="form-group">
                        <input v-model="email" type="text" placeholder="Email" class="form-control">
                        <div class="errors" v-if="errors.email">
                            <small class="text-danger" :key="error" v-for="error in errors.email">{{error}}</small>
                        </div>
                    </div>
                    <div class="form-group">
                        <input v-model="password" type="password" placeholder="Password" class="form-control">
                        <div class="errors" v-if="errors.password">
                            <small class="text-danger" :key="error" v-for="error in errors.password">{{error}}</small>
                        </div>
                    </div>
                    <div class="form-group">
                        <button @click="registerUser()" class="btn btn-success form-control">Sign Up</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import Axios from 'axios'

    export default {
        data() {
            return{
                name: '',
                email: '',
                password: '',
                errors: {}
            }
        },
        methods: {
            registerUser(){
                console.log(this.name, this.email, this.password);
                Axios.post('https://react-blog-api.bahdcasts.com/api/auth/register', {
                    name: this.name, email: this.email, password: this.password
                })
                .then((resp) => {
                    const { data } = resp.data;
                    localStorage.setItem('auth', JSON.stringify(data))
                    this.$root.auth = data;

                    this.$router.push('home');
                    //console.log(resp);
                })
                .catch(({ response }) => {
                    this.errors = response.data;
                    //console.log(error);
                });
            }
        }
    }
</script>