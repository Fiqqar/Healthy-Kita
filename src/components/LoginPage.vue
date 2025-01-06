<template>
    <div class="container-fluid bg-light min-vh-100 d-flex align-items-center justify-content-center py-5">
        <div class="card shadow-sm" style="max-width: 400px;">
            <div class="card-body p-4">
                <div class="text-center mb-4">
                    <h2 class="fw-bold">Login</h2>
                    <p class="text-muted">
                        Atau
                        <router-link to="/register" class="text-success text-decoration-none">
                            Buat Akun Baru
                        </router-link>
                    </p>
                </div>

                    <div class="mb-3">
                        <label for="username" class="form-label">Username</label>
                        <input type="text" class="form-control" id="username" required placeholder="Masukkan nama mu"
                            v-model="loginData.username" />
                    </div>

                    <div class="mb-3">
                        <label for="password" class="form-label">Password</label>
                        <input type="password" class="form-control" id="password" required
                            placeholder="Masukkan Password" v-model="loginData.password" />
                    </div>

                    <div class="mb-3 d-flex justify-content-between align-items-center">
                        <div class="form-check me-1">
                            <input class="form-check-input border-success cekboks" type="checkbox" id="remember-me"
                                value="true" v-model="loginData.rememberMe" />
                            <label class="form-check-label" for="remember-me">
                                Remember me
                            </label>
                        </div>
                        <a href="#" class="text-success text-decoration-none">Lupa password?</a>
                    </div>

                    <button type="submit" class="btn btn-success w-100 animate" @click="loginMethods">
                        Login
                    </button>
                    <h3 class="text-center" v-if="success">berhasil</h3>
                    <h3 class="text-center" v-if="error">error</h3>
            </div>
        </div>
    </div>
</template>


<script>
import axios from 'axios';
import textFile from '!!raw-loader!./file.txt';
export default {
    name: 'LoginPage',
    data() {
        return {
            arr: textFile,
            loginData: {
                username: "",
                password: "",
                rememberMe: false
            },
            success: false,
            error: false,
            response: {}
        }
    },
    methods: {
        loginMethods() {
            this.success = false;
            this.error = false;
            const { username, password, rememberMe } = this.loginData;
            if (!username || !password) {
                alert("Please fill out all required fields.");
                return;
            }
            axios.post(`${this.arr}/api/login/user`, {
                username: username,
                password: password,
                remember: rememberMe
            }, {
                headers: {
                    'Content-Type': 'application/json'
                },
                withCredentials: true
            })
                .then(response => {
                    this.success = true;
                this.response = response.data;
                this.userData = {
                    username: "",
                    email: "",
                    password: "",
                    confirmpw: ""
                };
                this.loading = false;  // Stop loading when request is successful

                const encKeyFetch = axios.get(`${arr}/oauth/encKey/get`,{
                withCredentials: true
                });
                const encKey = encKeyFetch.data.encKey;
                const ivKey = encKeyFetch.data.ivKey;
                const dbRequest = indexedDB.open('userKeysDB', 1);

                dbRequest.onupgradeneeded = (event) => {
                    let db = event.target.result;
                    if (!db.objectStoreNames.contains('keys')) {
                        db.createObjectStore('keys', { keyPath: 'id' });
                    }
                };
                dbRequest.onsuccess = (event) => {
                    const db = event.target.result;
                    const transaction = db.transaction('keys', 'readwrite');
                    const store = transaction.objectStore('keys');
                    store.put({ id: 'encKey', value: encKey });
                    store.put({ id: 'ivKey', value: ivKey });
                    transaction.oncomplete = () => {
                        console.log('encKey and ivKey stored successfully');
                    };
                };

        dbRequest.onerror = (event) => {
            console.error('Error on opening IndexedDB:', event.target.error);
        };

            })
                .catch(error => {
                    this.error = true;
                    console.error("There was an error:", error);
                });

        }
    },
}
</script>

<style scoped>
.animate {
    transition: all 0.3s ease;
}

.animate:hover {
    transform: scale(1.05);
}

.animate:active {
    transform: scale(0.95);
}

.cekboks {
    cursor: pointer;
}

.card {
    border-radius: 50px;
}
</style>
