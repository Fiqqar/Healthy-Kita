<template>
    <div class="container-fluid bg-light min-vh-100 d-flex align-items-center justify-content-center py-5">
        <div class="card shadow-sm" style="max-width: 400px;">
            <div class="card-body p-4">
                <div class="text-center mb-4">
                    <h2 class="fw-bold">Sign in</h2>
                    <p class="text-muted">
                        Or
                        <router-link to="/register" class="text-success text-decoration-none">
                            create a new account
                        </router-link>
                    </p>
                </div>

                <form>
                    <div class="mb-3">
                        <label for="email" class="form-label">Email address</label>
                        <input type="email" class="form-control" id="email" required
                            placeholder="youremail@example.com" />
                    </div>

                    <div class="mb-3">
                        <label for="password" class="form-label">Password</label>
                        <input type="password" class="form-control" id="password" required
                            placeholder="Enter your password" />
                    </div>

                    <div class="mb-3 d-flex justify-content-between align-items-center">
                        <div class="form-check me-1">
                            <input class="form-check-input border-success" type="checkbox" id="remember-me" />
                            <label class="form-check-label" for="remember-me">
                                Remember me
                            </label>
                        </div>
                        <a href="#" class="text-success text-decoration-none">Forgot password?</a>
                    </div>

                    <button type="submit" class="btn btn-success w-100 animate">
                        Sign in
                    </button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>


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
</style>