<script setup lang="ts">
import { ArrowLeft, ChartNoAxesCombined, CheckCircle2, FileText, Grid2X2, KeyRound, Mail, ShieldCheck } from 'lucide-vue-next'
import { ref } from 'vue'

import { Button } from '@/components/ui/button'
import { Input } from '@/components/ui/input'

defineEmits<{
  authenticated: []
  back: []
}>()

const dni = ref('')
const password = ref('')
const remember = ref(false)
</script>

<template>
  <main class="grid min-h-screen bg-[#111317] text-white lg:grid-cols-[0.8fr_1fr]">
    <section class="grid place-items-center px-6 py-10">
      <div class="w-full max-w-sm">
        <Button class="mb-8 border-white/10 bg-transparent text-white hover:bg-white/8" variant="outline" @click="$emit('back')">
          <ArrowLeft class="h-4 w-4" />
          Ir Inicio
        </Button>

        <div class="grid gap-7">
          <div class="grid justify-items-center gap-3 text-center">
            <img class="h-12 w-auto object-contain" src="/img/iconoTukuyAcademy.png" alt="Tukuy Academy" />
            <div>
              <h1 class="text-3xl font-black tracking-normal">Bienvenido de nuevo</h1>
              <p class="mt-3 text-sm text-slate-400">Ingresa tu DNI y clave para continuar</p>
            </div>
          </div>

          <form class="grid gap-5" @submit.prevent="$emit('authenticated')">
            <label class="grid gap-2 text-sm text-slate-400">
              DNI
              <Input
                v-model="dni"
                class="border-white/15 bg-black/30 text-white placeholder:text-slate-500 focus-visible:ring-blue-500"
                placeholder="Ingrese su DNI"
              />
            </label>

            <label class="grid gap-2 text-sm text-slate-400">
              Clave
              <Input
                v-model="password"
                class="border-white/15 bg-black/30 text-white placeholder:text-slate-500 focus-visible:ring-blue-500"
                placeholder="Contraseña"
                type="password"
              />
            </label>

            <div class="flex items-center justify-between text-xs">
              <label class="flex items-center gap-2 text-slate-300">
                <input v-model="remember" class="h-3.5 w-3.5 accent-blue-600" type="checkbox" />
                Recuérdame
              </label>
              <button class="text-blue-400 hover:text-blue-300" type="button">¿Olvidaste tu clave?</button>
            </div>

            <Button class="h-11 bg-blue-600 text-white hover:bg-blue-700" type="submit">Iniciar Sesión</Button>

            <div class="grid grid-cols-[1fr_auto_1fr] items-center gap-3 text-xs text-slate-500">
              <span class="h-px bg-white/10" />
              <span>O</span>
              <span class="h-px bg-white/10" />
            </div>

            <Button class="border-white/15 bg-transparent text-slate-200 hover:bg-white/8" variant="outline" type="button">
              <Mail class="h-4 w-4" />
              Iniciar con Google
            </Button>
          </form>

          <div class="grid gap-1 text-center text-xs text-slate-500">
            <span>© Tukuy Academy · Ver. 07.06</span>
            <span>Soporte: 910104133 · 930132386 · 974977988 · 930804475</span>
          </div>
        </div>
      </div>
    </section>

    <section class="hidden bg-[#17447d] px-8 py-10 lg:grid lg:place-items-center">
      <div class="grid w-full max-w-5xl gap-7">
        <div class="grid justify-items-center gap-3 text-center">
          <h2 class="text-2xl font-black tracking-normal">Tukuy Academy</h2>
          <p class="max-w-2xl text-sm text-blue-100/80">
            Desde la capacitación en el sistema Tukuy Obra hasta la generación de CV inteligente y oportunidades laborales.
          </p>
        </div>

        <div class="rounded-lg bg-white p-8 shadow-2xl">
          <div class="grid gap-8 lg:grid-cols-[120px_1fr] lg:items-center">
            <div class="grid gap-8 text-blue-700">
              <FileText class="h-12 w-12" />
              <ShieldCheck class="h-12 w-12" />
              <ChartNoAxesCombined class="h-12 w-12" />
              <Grid2X2 class="h-12 w-12" />
            </div>

            <div class="overflow-hidden rounded-xl border-[14px] border-slate-900 bg-slate-50">
              <div class="grid min-h-[360px] grid-cols-[190px_1fr]">
                <aside class="bg-[#0f4c9a] p-5 text-white">
                  <div class="mb-8 flex items-center gap-3">
                    <img class="h-10 w-auto object-contain" src="/img/iconoTukuyAcademy.png" alt="Tukuy Academy" />
                    <strong class="leading-tight">TUKUY<br />ACADEMY</strong>
                  </div>
                  <div class="grid gap-3 text-sm text-blue-100">
                    <span>Panel General</span>
                    <span>Expediente técnico</span>
                    <span>Cuaderno digital</span>
                    <span>Valorizaciones</span>
                    <span>Bolsa laboral</span>
                  </div>
                </aside>

                <div class="grid gap-5 p-6 text-slate-900">
                  <div class="grid grid-cols-4 gap-4">
                    <div class="rounded-lg border border-slate-200 bg-white p-4 text-center">
                      <CheckCircle2 class="mx-auto mb-2 h-6 w-6 text-blue-600" />
                      <strong class="block text-2xl">43</strong>
                      <span class="text-xs text-slate-500">Cursos activos</span>
                    </div>
                    <div class="rounded-lg border border-slate-200 bg-white p-4 text-center">
                      <KeyRound class="mx-auto mb-2 h-6 w-6 text-amber-500" />
                      <strong class="block text-2xl">5</strong>
                      <span class="text-xs text-slate-500">Alertas</span>
                    </div>
                    <div class="rounded-lg border border-slate-200 bg-white p-4 text-center">
                      <strong class="block text-2xl">91%</strong>
                      <span class="text-xs text-slate-500">Compatibilidad</span>
                    </div>
                    <div class="rounded-lg border border-slate-200 bg-white p-4 text-center">
                      <strong class="block text-2xl">158</strong>
                      <span class="text-xs text-slate-500">Usuarios demo</span>
                    </div>
                  </div>

                  <div class="grid gap-4 lg:grid-cols-[1fr_0.8fr]">
                    <div class="rounded-lg border border-slate-200 bg-white p-5">
                      <h3 class="font-bold">Informe de avance</h3>
                      <div class="mt-6 h-24 rounded-md bg-gradient-to-r from-blue-100 via-blue-200 to-blue-500" />
                      <div class="mt-3 flex justify-between text-xs text-slate-500">
                        <span>Feb</span><span>Mar</span><span>Abr</span><span>May</span><span>Jun</span>
                      </div>
                    </div>
                    <div class="rounded-lg border border-slate-200 bg-white p-5">
                      <h3 class="font-bold">Noticias de formación</h3>
                      <div class="mt-4 grid gap-3 text-sm">
                        <span class="rounded-md bg-blue-50 p-3">Nueva ruta: valorizaciones y reportes</span>
                        <span class="rounded-md bg-blue-50 p-3">CV inteligente conectado al perfil</span>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
