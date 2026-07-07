<script setup lang="ts">
import { Award, BookOpen, BriefcaseBusiness, ChevronRight, Mail, MapPin, Phone, Search } from 'lucide-vue-next'
import { computed, ref } from 'vue'

import SiteFooter from '@/components/shared/SiteFooter.vue'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card'
import { Input } from '@/components/ui/input'
import { carouselSlides, courses, heroImage, tukuyModules } from '@/data/academy'

defineEmits<{ login: [] }>()

const searchTerm = ref('')
const filteredCourses = computed(() => {
  const term = searchTerm.value.trim().toLowerCase()
  if (!term) return courses
  return courses.filter((course) =>
    [course.title, course.category, course.level, course.mode].some((value) => value.toLowerCase().includes(term)),
  )
})

function scrollToSection(id: string) {
  const section = document.querySelector<HTMLElement>(id)
  if (!section) return

  const headerOffset = 88
  const start = window.scrollY
  const target = section.getBoundingClientRect().top + window.scrollY - headerOffset
  const distance = target - start
  const duration = 950
  const startTime = performance.now()

  function easeInOutCubic(progress: number) {
    return progress < 0.5 ? 4 * progress ** 3 : 1 - Math.pow(-2 * progress + 2, 3) / 2
  }

  function animate(currentTime: number) {
    const elapsed = currentTime - startTime
    const progress = Math.min(elapsed / duration, 1)
    window.scrollTo(0, start + distance * easeInOutCubic(progress))

    if (progress < 1) {
      window.requestAnimationFrame(animate)
    }
  }

  window.requestAnimationFrame(animate)
}
</script>

<template>
  <header class="sticky top-0 z-20 border-b border-[#D6E2EF] bg-[#EAF1F8]/95 text-[#07152B] shadow-sm backdrop-blur">
    <div class="mx-auto flex max-w-7xl items-center justify-between gap-4 px-5 py-4">
      <button class="flex cursor-pointer items-center gap-3 text-left" type="button">
        <img class="h-11 w-auto object-contain" src="/img/iconoTukuyAcademy.png" alt="Tukuy Academy" />
        <div>
          <strong class="block text-xl leading-none tracking-normal text-[#07152B]">
            <span class="font-black">Tukuy</span>
            <span class="font-light"> Academy</span>
          </strong>
          <span class="text-sm text-[#52657A]">Formación y empleabilidad</span>
        </div>
      </button>

      <nav class="hidden items-center gap-1 md:flex">
        <button class="rounded-md px-3 py-2 text-sm font-semibold text-[#52657A] transition hover:bg-[#DDEAF7] hover:text-[#07152B]" type="button" @click="scrollToSection('#cursos')">Cursos</button>
        <button class="rounded-md px-3 py-2 text-sm font-semibold text-[#52657A] transition hover:bg-[#DDEAF7] hover:text-[#07152B]" type="button" @click="scrollToSection('#modulos')">Módulos</button>
        <button class="rounded-md px-3 py-2 text-sm font-semibold text-[#52657A] transition hover:bg-[#DDEAF7] hover:text-[#07152B]" type="button" @click="scrollToSection('#oportunidades')">Oportunidades</button>
        <button class="rounded-md px-3 py-2 text-sm font-semibold text-[#52657A] transition hover:bg-[#DDEAF7] hover:text-[#07152B]" type="button" @click="scrollToSection('#contacto')">Contacto</button>
      </nav>

      <Button @click="$emit('login')">Acceder</Button>
    </div>
  </header>

  <main class="bg-slate-950 text-white">
    <section class="relative overflow-hidden">
      <img :src="heroImage" alt="Formación laboral para personas de obra" class="absolute inset-0 h-full w-full object-cover opacity-45" />
      <div class="absolute inset-0 bg-gradient-to-br from-slate-950 via-slate-950/82 to-blue-950/70" />

      <div class="relative mx-auto grid max-w-7xl gap-10 px-5 py-12 lg:grid-cols-[1.05fr_0.95fr] lg:items-center lg:py-20">
        <div class="grid gap-7">
          <Badge class="w-fit border-white/20 bg-white/10 text-white" variant="outline">Academy & Jobs</Badge>

          <div class="grid gap-4">
            <h1 class="max-w-4xl text-4xl font-black tracking-normal sm:text-6xl">
              Aprende a gestionar obras con Tukuy Obra y potencia tu perfil.
            </h1>
            <p class="max-w-2xl text-base leading-7 text-white/72 sm:text-lg">
              Tukuy Academy capacita a residentes, asistentes, almaceneros y equipos técnicos en el uso del software
              Tukuy Obra: avance físico y financiero, cuaderno digital, valorizaciones, reportes e inteligencia
              artificial aplicada a obra.
            </p>
          </div>

          <div class="relative max-w-2xl">
            <Search class="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-white/45" />
            <Input
              v-model="searchTerm"
              class="h-12 border-white/15 bg-white/10 pl-10 text-white placeholder:text-white/50 focus-visible:ring-white/40"
              type="search"
              placeholder="Buscar cursos de avance de obra, valorizaciones, almacén, IA o CV..."
            />
          </div>

          <div class="flex flex-wrap gap-3">
            <Button size="lg" @click="$emit('login')">
              Acceder al portal <ChevronRight class="h-4 w-4" />
            </Button>
            <Button class="border-white/20 bg-white/10 text-white hover:bg-white/15" variant="outline" size="lg" @click="scrollToSection('#cursos')">
              Ver cursos destacados
            </Button>
          </div>

          <div class="grid gap-3 sm:grid-cols-3">
            <div class="rounded-lg border border-white/10 bg-white/8 p-4 backdrop-blur">
              <strong class="block text-2xl">9</strong>
              <span class="text-sm text-white/65">cursos simulados de obra</span>
            </div>
            <div class="rounded-lg border border-white/10 bg-white/8 p-4 backdrop-blur">
              <strong class="block text-2xl">91%</strong>
              <span class="text-sm text-white/65">matching laboral demo</span>
            </div>
            <div class="rounded-lg border border-white/10 bg-white/8 p-4 backdrop-blur">
              <strong class="block text-2xl">3</strong>
              <span class="text-sm text-white/65">certificados simulados</span>
            </div>
          </div>
        </div>

        <div class="grid gap-4">
          <div class="relative overflow-hidden rounded-lg border border-white/15 bg-white/10 shadow-2xl backdrop-blur">
            <div class="flex animate-[academy-slide_14s_ease-in-out_infinite]">
              <article v-for="slide in carouselSlides" :key="slide.title" class="relative min-h-[440px] min-w-full overflow-hidden">
                <img :src="slide.image" :alt="slide.title" class="absolute inset-0 h-full w-full object-cover" />
                <div class="absolute inset-0 bg-gradient-to-t from-slate-950/92 via-slate-950/28 to-transparent" />
                <div class="absolute inset-x-0 bottom-0 grid gap-3 p-6">
                  <Badge class="w-fit border-white/20 bg-white/90 text-slate-950" variant="outline">{{ slide.label }}</Badge>
                  <h2 class="text-3xl font-black tracking-normal">{{ slide.title }}</h2>
                  <p class="max-w-md text-sm leading-6 text-white/75">{{ slide.description }}</p>
                </div>
              </article>
            </div>
          </div>
          <div class="grid grid-cols-3 gap-2">
            <div v-for="slide in carouselSlides" :key="slide.label" class="h-1.5 overflow-hidden rounded-full bg-white/15">
              <span class="block h-full rounded-full bg-white/80" />
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="beneficios" class="mx-auto grid max-w-7xl gap-4 px-5 py-10 md:grid-cols-3">
      <Card class="border-white/10 bg-white/8 text-white backdrop-blur">
        <CardHeader>
          <BookOpen class="h-5 w-5 text-blue-300" />
          <CardTitle>Gestión de obras</CardTitle>
          <CardDescription class="text-white/65">Cursos para avance físico-financiero, cuaderno digital, valorizaciones y reportes técnicos.</CardDescription>
        </CardHeader>
      </Card>
      <Card class="border-white/10 bg-white/8 text-white backdrop-blur">
        <CardHeader>
          <Award class="h-5 w-5 text-teal-300" />
          <CardTitle>Dominio del sistema</CardTitle>
          <CardDescription class="text-white/65">Capacitación práctica para usar Tukuy Obra, Tukuy Almacén, asistencia y paneles de control.</CardDescription>
        </CardHeader>
      </Card>
      <Card class="border-white/10 bg-white/8 text-white backdrop-blur">
        <CardHeader>
          <BriefcaseBusiness class="h-5 w-5 text-amber-300" />
          <CardTitle>Empleabilidad conectada</CardTitle>
          <CardDescription class="text-white/65">Tu experiencia usando el sistema alimenta tu CV inteligente y mejora el matching laboral.</CardDescription>
        </CardHeader>
      </Card>
    </section>

    <section id="modulos" class="mx-auto grid max-w-7xl gap-6 px-5 pb-14">
      <div class="grid gap-3 md:grid-cols-[1fr_0.75fr] md:items-end">
        <div>
          <p class="text-xs font-bold uppercase text-teal-300 ">Ecosistema Tukuy Obra</p>
          <h2 class="mt-2 max-w-3xl text-3xl font-black tracking-normal">Todo lo que tu obra necesita</h2>
        </div>
      </div>

      <div class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
        <Card v-for="module in tukuyModules" :key="module.title" class="group overflow-hidden border-white/10 bg-white/8 text-white backdrop-blur">
          <div class="relative h-24 overflow-hidden border-b border-white/10 bg-gradient-to-br from-white/16 via-blue-400/12 to-teal-400/14">
            <div class="absolute left-4 top-4 grid h-12 w-12 place-items-center rounded-lg border border-white/15 bg-white/12 text-2xl backdrop-blur transition group-hover:scale-105">
              {{ module.icon }}
            </div>
            <div class="absolute bottom-3 right-3 rounded-full bg-white/10 px-3 py-1 text-xs font-semibold text-white/75">
              Curso módulo
            </div>
          </div>
          <CardHeader>
            <CardTitle class="text-lg">{{ module.title }}</CardTitle>
            <CardDescription class="min-h-12 text-white/65">{{ module.description }}</CardDescription>
          </CardHeader>
          <CardContent class="grid gap-4">
            <div class="flex flex-wrap gap-2">
              <Badge v-for="tag in module.tags" :key="tag" class="border-white/20 bg-white/90 text-slate-950" variant="outline">
                {{ tag }}
              </Badge>
            </div>
            <Button class="w-full border-white/20 bg-white/10 text-white hover:bg-white/15" variant="outline" @click="$emit('login')">
              Ver ruta
            </Button>
          </CardContent>
        </Card>
      </div>
    </section>

    <section id="oportunidades" class="mx-auto grid max-w-7xl gap-5 px-5 pb-14">
      <div class="grid gap-3 md:grid-cols-[1fr_0.75fr] md:items-end">
        <div>
          <p class="text-xs font-bold uppercase text-teal-300">Cursos por perfil</p>
          <h2 class="mt-2 max-w-3xl text-3xl font-black tracking-normal">Rutas modernas para operar y crecer</h2>
        </div>
        <p class="text-sm leading-6 text-white/68">
          Cada ruta combina uso del sistema, evidencia de experiencia y competencias para postular a mejores cargos.
        </p>
      </div>

      <div class="grid gap-4 lg:grid-cols-3">
        <Card class="overflow-hidden border-white/10 bg-white/8 text-white backdrop-blur">
          <CardHeader>
            <Badge class="w-fit border-white/20 bg-white/90 text-slate-950" variant="outline">Operativo</Badge>
            <CardTitle>Almacén, pedidos y requerimientos</CardTitle>
            <CardDescription class="text-white/65">Para auxiliares, responsables de materiales y asistentes logísticos.</CardDescription>
          </CardHeader>
          <CardContent class="flex flex-wrap gap-2">
            <Badge variant="outline" class="border-white/20 text-blue-500">Inventario</Badge>
            <Badge variant="outline" class="border-white/20 text-blue-500">Compras</Badge>
            <Badge variant="outline" class="border-white/20 text-blue-500">Trazabilidad</Badge>
          </CardContent>
        </Card>

        <Card class="overflow-hidden border-white/10 bg-white/8 text-white backdrop-blur">
          <CardHeader>
            <Badge class="w-fit border-white/20 bg-white/90 text-slate-950" variant="outline">Técnico</Badge>
            <CardTitle>Avance, valorizaciones y reportes</CardTitle>
            <CardDescription class="text-white/65">Para residentes, asistentes técnicos y control de obra.</CardDescription>
          </CardHeader>
          <CardContent class="flex flex-wrap gap-2">
            <Badge variant="outline" class="border-white/20 text-blue-500">Curva S</Badge>
            <Badge variant="outline" class="border-white/20 text-blue-500">KPI</Badge>
            <Badge variant="outline" class="border-white/20 text-blue-500">PDF / Excel</Badge>
          </CardContent>
        </Card>

        <Card class="overflow-hidden border-white/10 bg-white/8 text-white backdrop-blur">
          <CardHeader>
            <Badge class="w-fit border-white/20 bg-white/90 text-slate-950" variant="outline">Inteligente</Badge>
            <CardTitle>IA, BIM y análisis de obra</CardTitle>
            <CardDescription class="text-white/65">Para equipos que necesitan interpretar datos y tomar mejores decisiones.</CardDescription>
          </CardHeader>
          <CardContent class="flex flex-wrap gap-2">
            <Badge variant="outline" class="border-white/20 text-blue-500">Tukuy IA</Badge>
            <Badge variant="outline" class="border-white/20 text-blue-500">BIM</Badge>
            <Badge variant="outline" class="border-white/20 text-blue-500">Comparativas</Badge>
          </CardContent>
        </Card>
      </div>
    </section>

    <section id="cursos" class="mx-auto grid max-w-7xl gap-5 px-5 pb-14">
      <div class="flex items-end justify-between gap-4">
        <div>
          <p class="text-xs font-bold uppercase text-teal-300">Cursos destacados</p>
          <h2 class="text-3xl font-black tracking-normal">Empieza con una ruta práctica</h2>
        </div>
        <Button class="hidden border-white/20 bg-white/10 text-white hover:bg-white/15 sm:inline-flex" variant="outline" @click="$emit('login')">
          Ingresar y ver todo
        </Button>
      </div>

      <div class="grid gap-4 md:grid-cols-2 xl:grid-cols-4">
        <Card v-for="course in filteredCourses" :key="course.id" class="group overflow-hidden border-white/10 bg-white/8 text-white backdrop-blur">
          <div class="relative h-36 overflow-hidden">
            <img :src="course.image" :alt="course.title" class="h-full w-full object-cover transition duration-500 group-hover:scale-105" />
            <div :class="['absolute inset-0 bg-gradient-to-br opacity-50', course.imageTone]" />
            <Badge class="absolute left-4 top-4 border-white/20 bg-white/90 text-slate-950" variant="outline">{{ course.level }}</Badge>
          </div>
          <CardHeader>
            <CardTitle>{{ course.title }}</CardTitle>
            <CardDescription class="text-white/65">{{ course.category }} · {{ course.duration }} · {{ course.mode }}</CardDescription>
          </CardHeader>
          <CardContent>
            <Button class="w-full bg-white text-slate-950 hover:bg-white/90" @click="$emit('login')">Comenzar gratis</Button>
          </CardContent>
        </Card>
      </div>
    </section>

    <section id="contacto" class="mx-auto grid max-w-7xl gap-5 px-5 pb-14">
      <Card class="overflow-hidden border-white/10 bg-white/8 text-white backdrop-blur">
        <CardContent class="grid gap-6 p-6 lg:grid-cols-[1fr_0.9fr] lg:items-center">
          <div class="grid gap-3">
            <p class="text-xs font-bold uppercase text-teal-300">Contacto</p>
            <h2 class="text-3xl font-black tracking-normal">Conversemos sobre capacitación para tu equipo de obra</h2>
            <p class="max-w-2xl text-sm leading-6 text-white/68">
              Simula una solicitud para capacitar residentes, asistentes, almaceneros, responsables de cuadrilla y
              equipos técnicos en el uso de Tukuy Obra.
            </p>
          </div>

          <div class="grid gap-3 text-sm">
            <div class="flex items-center gap-3 rounded-lg border border-white/10 bg-white/8 p-3">
              <MapPin class="h-4 w-4 text-teal-300" />
              <span>Cusco, Perú</span>
            </div>
            <div class="flex items-center gap-3 rounded-lg border border-white/10 bg-white/8 p-3">
              <Phone class="h-4 w-4 text-teal-300" />
              <span>+51 930 804 475</span>
            </div>
            <div class="flex items-center gap-3 rounded-lg border border-white/10 bg-white/8 p-3">
              <Mail class="h-4 w-4 text-teal-300" />
              <span>academy@tukuyobra.com</span>
            </div>
            <Button class="mt-2 bg-white text-slate-950 hover:bg-white/90" @click="$emit('login')">Solicitar demo de capacitación</Button>
          </div>
        </CardContent>
      </Card>
    </section>

    <SiteFooter variant="dark" />
  </main>
</template>
