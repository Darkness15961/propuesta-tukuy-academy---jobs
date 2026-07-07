<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'

import LoginView from '@/views/LoginView.vue'
import PublicLanding from '@/views/PublicLanding.vue'
import UserPortal from '@/views/UserPortal.vue'

const isAuthenticated = ref(false)
const currentPath = ref(window.location.pathname)

function navigate(path: string) {
  window.history.pushState({}, '', path)
  currentPath.value = path
}

function login() {
  isAuthenticated.value = true
  navigate('/app')
}

function goToLanding() {
  isAuthenticated.value = false
  navigate('/')
}

function goToLogin() {
  navigate('/login')
}

function handlePopState() {
  currentPath.value = window.location.pathname
  if (currentPath.value !== '/app') {
    isAuthenticated.value = false
  }
}

onMounted(() => {
  window.addEventListener('popstate', handlePopState)
})

onUnmounted(() => {
  window.removeEventListener('popstate', handlePopState)
})
</script>

<template>
  <div class="min-h-screen bg-background text-foreground">
    <UserPortal v-if="isAuthenticated" @go-to-landing="goToLanding" />
    <LoginView v-else-if="currentPath === '/login'" @authenticated="login" @back="goToLanding" />
    <PublicLanding v-else @login="goToLogin" />
  </div>
</template>
