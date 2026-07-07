<script setup lang="ts">
import {
  Award,
  Bell,
  BriefcaseBusiness,
  CalendarCheck,
  ChevronRight,
  GraduationCap,
  Search,
  Sparkles,
} from 'lucide-vue-next'
import { computed, ref } from 'vue'

import PageTitle from '@/components/shared/PageTitle.vue'
import ProfileRow from '@/components/shared/ProfileRow.vue'
import SiteFooter from '@/components/shared/SiteFooter.vue'
import { Avatar, AvatarFallback } from '@/components/ui/avatar'
import { Badge } from '@/components/ui/badge'
import { Button } from '@/components/ui/button'
import { Card, CardContent, CardDescription, CardHeader, CardTitle } from '@/components/ui/card'
import { Input } from '@/components/ui/input'
import { Progress } from '@/components/ui/progress'
import { courses, heroImage, jobs, navItems, user, workExperiences } from '@/data/academy'
import type { Course, ViewId } from '@/types/academy'

defineEmits<{ goToLanding: [] }>()

const activeView = ref<ViewId>('home')
const searchTerm = ref('')

const filteredCourses = computed(() => {
  const term = searchTerm.value.trim().toLowerCase()
  if (!term) return courses
  return courses.filter((course) =>
    [course.title, course.category, course.level, course.mode].some((value) => value.toLowerCase().includes(term)),
  )
})

const activeCourses = computed(() => courses.filter((course) => course.status === 'En curso'))
const recommendedJobs = computed(() => jobs.filter((job) => job.match >= 80))

function courseBadgeVariant(status: Course['status']) {
  if (status === 'Completado') return 'success'
  if (status === 'En curso') return 'warning'
  return 'default'
}
</script>

<template>
  <header class="sticky top-0 z-20 border-b border-border bg-card/95 backdrop-blur">
    <div class="mx-auto flex max-w-7xl flex-col gap-4 px-5 py-4 lg:flex-row lg:items-center lg:justify-between">
      <div class="flex items-center justify-between gap-4">
        <button class="flex cursor-pointer items-center gap-3 text-left" type="button" @click="$emit('goToLanding')">
          <img class="h-11 w-auto object-contain" src="/img/iconoTukuyAcademy.png" alt="Tukuy Academy" />
          <div>
            <strong class="block text-xl leading-none tracking-normal text-slate-950">
              <span class="font-black">Tukuy</span>
              <span class="font-light"> Academy</span>
            </strong>
            <span class="text-sm text-muted-foreground">Aprende, certifícate y postula</span>
          </div>
        </button>

        <div class="flex items-center gap-2 lg:hidden">
          <Button variant="outline" size="icon">
            <Bell class="h-4 w-4" />
          </Button>
          <Avatar>
            <AvatarFallback>{{ user.initials }}</AvatarFallback>
          </Avatar>
        </div>
      </div>

      <nav class="flex gap-1 overflow-x-auto">
        <button
          v-for="item in navItems"
          :key="item.id"
          type="button"
          class="whitespace-nowrap rounded-md px-3 py-2 text-sm font-semibold text-muted-foreground transition hover:bg-muted hover:text-foreground"
          :class="activeView === item.id ? 'bg-blue-50 text-blue-700' : ''"
          @click="activeView = item.id"
        >
          {{ item.label }}
        </button>
      </nav>

      <div class="hidden items-center gap-3 lg:flex">
        <Button variant="outline" size="icon">
          <Bell class="h-4 w-4" />
        </Button>
        <button class="flex items-center gap-3 rounded-lg border border-border px-3 py-2 text-left" type="button" @click="activeView = 'profile'">
          <Avatar>
            <AvatarFallback>{{ user.initials }}</AvatarFallback>
          </Avatar>
          <div>
            <strong class="block text-sm">{{ user.name }}</strong>
            <span class="block text-xs text-muted-foreground">{{ user.trade }}</span>
          </div>
        </button>
      </div>
    </div>
  </header>

  <main>
    <section v-if="activeView === 'home'" class="mx-auto grid max-w-7xl gap-8 px-5 py-7 lg:py-10">
      <div class="grid overflow-hidden rounded-lg border border-border bg-card shadow-sm lg:grid-cols-[1.05fr_0.95fr]">
        <div class="grid content-center gap-6 p-6 sm:p-9 lg:p-12">
          <div class="flex flex-wrap items-center gap-2">
            <Badge class="w-fit" variant="default">Sesión iniciada</Badge>
            <Badge class="w-fit" variant="outline">Bienvenido, {{ user.name.split(' ')[0] }}</Badge>
          </div>
          <div class="grid gap-4">
            <h1 class="max-w-3xl text-4xl font-black tracking-normal text-slate-950 sm:text-5xl">
              Tu ruta para aprender, certificarte y conseguir mejores oportunidades.
            </h1>
            <p class="max-w-2xl text-base leading-7 text-muted-foreground">
              Continúa tus cursos, actualiza tu perfil laboral, genera tu CV y encuentra empleos alineados a tu experiencia en obra.
            </p>
          </div>
          <div class="relative max-w-2xl">
            <Search class="absolute left-3 top-1/2 h-4 w-4 -translate-y-1/2 text-muted-foreground" />
            <Input v-model="searchTerm" class="h-12 pl-10" type="search" placeholder="Buscar cursos, certificados u oportunidades..." />
          </div>
          <div class="flex flex-wrap gap-3">
            <Button size="lg" @click="activeView = 'learning'">
              Explorar cursos <ChevronRight class="h-4 w-4" />
            </Button>
            <Button variant="outline" size="lg" @click="activeView = 'jobs'">Ver oportunidades</Button>
          </div>
        </div>

        <div class="relative min-h-[420px] overflow-hidden bg-slate-950 p-6 text-white sm:p-9">
          <img :src="heroImage" alt="Profesional de construcción usando herramientas digitales" class="absolute inset-0 h-full w-full object-cover" />
          <div class="absolute inset-0 bg-gradient-to-br from-slate-950/92 via-slate-950/58 to-teal-900/64" />
          <div class="relative grid h-full content-between gap-6">
            <div class="ml-auto w-fit rounded-lg border border-white/20 bg-white/10 px-4 py-3 backdrop-blur">
              <span class="text-sm text-white/75">Mejor oportunidad detectada</span>
              <strong class="block text-3xl">{{ recommendedJobs[0]?.match ?? 0 }}%</strong>
              <span class="text-xs text-white/70">compatible con tu perfil</span>
            </div>
            <Card class="border-white/15 bg-white/95 text-foreground">
              <CardHeader>
                <CardDescription>Tu ruta sugerida</CardDescription>
                <CardTitle class="text-xl">Completa SST y postula a logística de obra</CardTitle>
              </CardHeader>
              <CardContent class="grid gap-4">
                <div>
                  <div class="mb-2 flex justify-between text-sm">
                    <span class="text-muted-foreground">Perfil laboral</span>
                    <strong>{{ user.profileProgress }}%</strong>
                  </div>
                  <Progress :model-value="user.profileProgress" />
                </div>
                <div class="grid grid-cols-3 gap-2 text-center text-sm">
                  <div class="rounded-md bg-slate-100 p-3"><strong class="block">{{ activeCourses.length }}</strong><span class="text-muted-foreground">Cursos</span></div>
                  <div class="rounded-md bg-slate-100 p-3"><strong class="block">{{ user.certificates }}</strong><span class="text-muted-foreground">Certificados</span></div>
                  <div class="rounded-md bg-slate-100 p-3"><strong class="block">{{ user.applications }}</strong><span class="text-muted-foreground">Postulaciones</span></div>
                </div>
              </CardContent>
            </Card>
          </div>
        </div>
      </div>

      <div class="grid gap-4 md:grid-cols-3">
        <Card>
          <CardHeader>
            <GraduationCap class="h-5 w-5 text-blue-700" />
            <CardTitle>Aprende a tu ritmo</CardTitle>
            <CardDescription>Cursos virtuales, presenciales y mixtos orientados a perfiles de obra.</CardDescription>
          </CardHeader>
        </Card>
        <Card>
          <CardHeader>
            <Award class="h-5 w-5 text-teal-700" />
            <CardTitle>Certifica tu avance</CardTitle>
            <CardDescription>Constancias y certificados verificables para fortalecer tu perfil laboral.</CardDescription>
          </CardHeader>
        </Card>
        <Card>
          <CardHeader>
            <BriefcaseBusiness class="h-5 w-5 text-amber-700" />
            <CardTitle>Postula mejor</CardTitle>
            <CardDescription>Oportunidades recomendadas según tus cursos, experiencia y disponibilidad.</CardDescription>
          </CardHeader>
        </Card>
      </div>

      <div class="grid gap-5 lg:grid-cols-[minmax(0,1fr)_360px]">
        <section class="grid gap-4">
          <div class="flex items-center justify-between gap-3">
            <div>
              <p class="text-xs font-bold uppercase text-secondary">Cursos recomendados</p>
              <h2 class="text-2xl font-bold tracking-normal">Continúa aprendiendo</h2>
            </div>
            <Button variant="ghost" @click="activeView = 'learning'">Ver todo</Button>
          </div>
          <div class="grid gap-4 md:grid-cols-2">
            <Card v-for="course in filteredCourses.slice(0, 4)" :key="course.id" class="group overflow-hidden">
              <div class="relative h-36 overflow-hidden">
                <img :src="course.image" :alt="course.title" class="h-full w-full object-cover transition duration-500 group-hover:scale-105" />
                <div :class="['absolute inset-0 bg-gradient-to-br opacity-45', course.imageTone]" />
                <Badge :variant="courseBadgeVariant(course.status)" class="absolute left-4 top-4">{{ course.status }}</Badge>
              </div>
              <CardHeader>
                <span class="text-xs font-semibold text-muted-foreground">{{ course.duration }}</span>
                <CardTitle>{{ course.title }}</CardTitle>
                <CardDescription>{{ course.category }} · {{ course.level }} · {{ course.mode }}</CardDescription>
              </CardHeader>
              <CardContent class="grid gap-3">
                <Progress :model-value="course.progress" />
                <Button variant="outline" class="w-full">{{ course.status === 'Disponible' ? 'Inscribirme' : 'Continuar' }}</Button>
              </CardContent>
            </Card>
          </div>
        </section>

        <aside class="grid gap-4">
          <Card>
            <CardHeader>
              <CardTitle>Tu perfil</CardTitle>
              <CardDescription>{{ user.specialty }} · {{ user.location }}</CardDescription>
            </CardHeader>
            <CardContent class="grid gap-4">
              <div>
                <div class="mb-2 flex justify-between text-sm">
                  <span class="text-muted-foreground">Completitud</span>
                  <strong>{{ user.profileProgress }}%</strong>
                </div>
                <Progress :model-value="user.profileProgress" />
              </div>
              <div>
                <div class="mb-2 flex justify-between text-sm">
                  <span class="text-muted-foreground">Empleabilidad</span>
                  <strong>{{ user.employabilityScore }}%</strong>
                </div>
                <Progress :model-value="user.employabilityScore" />
              </div>
              <Button class="w-full" variant="outline" @click="activeView = 'profile'">Actualizar perfil</Button>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle>Próxima acción</CardTitle>
              <CardDescription>Recomendación personalizada</CardDescription>
            </CardHeader>
            <CardContent class="grid gap-3 text-sm">
              <div class="flex gap-3 rounded-lg border border-border p-3">
                <Sparkles class="mt-0.5 h-4 w-4 text-blue-700" />
                <span>Agrega una referencia laboral para mejorar tu CV.</span>
              </div>
              <div class="flex gap-3 rounded-lg border border-border p-3">
                <CalendarCheck class="mt-0.5 h-4 w-4 text-teal-700" />
                <span>Completa tu evaluación SST antes del viernes.</span>
              </div>
            </CardContent>
          </Card>
        </aside>
      </div>
    </section>

    <section v-else-if="activeView === 'learning'" class="mx-auto grid max-w-7xl gap-6 px-5 py-7">
      <PageTitle eyebrow="Mi aprendizaje" title="Cursos y progreso" description="Gestiona los cursos en los que estás inscrito y descubre nuevas rutas." />
      <div class="grid gap-4 md:grid-cols-2 xl:grid-cols-3">
        <Card v-for="course in courses" :key="course.id" class="group overflow-hidden">
          <div class="relative h-40 overflow-hidden">
            <img :src="course.image" :alt="course.title" class="h-full w-full object-cover transition duration-500 group-hover:scale-105" />
            <div :class="['absolute inset-0 bg-gradient-to-br opacity-45', course.imageTone]" />
            <Badge :variant="courseBadgeVariant(course.status)" class="absolute left-4 top-4">{{ course.status }}</Badge>
          </div>
          <CardHeader>
            <CardTitle>{{ course.title }}</CardTitle>
            <CardDescription>{{ course.category }} · {{ course.duration }} · {{ course.mode }}</CardDescription>
          </CardHeader>
          <CardContent class="grid gap-3">
            <Progress :model-value="course.progress" />
            <Button>{{ course.status === 'Disponible' ? 'Inscribirme' : 'Continuar curso' }}</Button>
          </CardContent>
        </Card>
      </div>
    </section>

    <section v-else-if="activeView === 'jobs'" class="mx-auto grid max-w-7xl gap-6 px-5 py-7">
      <PageTitle eyebrow="Oportunidades" title="Trabajos recomendados para ti" description="Postulaciones alineadas con tu perfil, cursos y disponibilidad." />
      <div class="grid gap-4">
        <Card v-for="job in jobs" :key="job.id">
          <CardContent class="grid gap-4 p-5 md:grid-cols-[1fr_auto] md:items-center">
            <div class="grid gap-3">
              <div>
                <Badge variant="success">{{ job.match }}% compatible</Badge>
                <h3 class="mt-3 text-xl font-bold">{{ job.title }}</h3>
                <p class="mt-1 text-sm text-muted-foreground">{{ job.company }} · {{ job.location }} · vence {{ job.deadline }}</p>
              </div>
              <div class="flex flex-wrap gap-2">
                <Badge v-for="tag in job.tags" :key="tag" variant="outline">{{ tag }}</Badge>
              </div>
            </div>
            <Button>Postular ahora</Button>
          </CardContent>
        </Card>
      </div>
    </section>

    <section v-else-if="activeView === 'cv'" class="mx-auto grid max-w-7xl gap-6 px-5 py-7">
      <PageTitle eyebrow="CV inteligente" title="Tu CV listo para postular" description="Genera un CV claro usando cursos, certificados y experiencia importada desde Tukuy Obra/SIADEG." />
      <div class="grid gap-5 lg:grid-cols-[380px_1fr]">
        <Card>
          <CardHeader>
            <CardTitle>Datos disponibles</CardTitle>
            <CardDescription>La IA simulada detecta lo que falta antes de exportar.</CardDescription>
          </CardHeader>
          <CardContent class="grid gap-3 text-sm">
            <ProfileRow label="Especialidad" :value="user.specialty" />
            <ProfileRow label="Experiencias" :value="`${workExperiences.length}`" />
            <ProfileRow label="Fuentes conectadas" value="Tukuy Obra / SIADEG" />
            <ProfileRow label="Certificados" :value="`${user.certificates}`" />
            <ProfileRow label="Postulaciones" :value="`${user.applications}`" />
            <ProfileRow label="Pendiente" value="Validar experiencia manual" />
            <Button><Sparkles class="h-4 w-4" /> Mejorar resumen</Button>
          </CardContent>
        </Card>

        <Card class="border-l-4 border-l-primary">
          <CardHeader>
            <div class="flex items-center gap-3">
              <Avatar class="h-14 w-14"><AvatarFallback>{{ user.initials }}</AvatarFallback></Avatar>
              <div>
                <CardTitle>{{ user.name }}</CardTitle>
                <CardDescription>{{ user.trade }} · {{ user.location }}</CardDescription>
              </div>
            </div>
          </CardHeader>
          <CardContent class="grid gap-4">
            <div>
              <h3 class="font-semibold">Resumen profesional</h3>
              <p class="mt-2 text-sm leading-6 text-muted-foreground">
                Profesional con experiencia en almacén y logística de obra, control de materiales, seguimiento de
                requerimientos y uso de módulos operativos de Tukuy Obra. Ha participado en {{ workExperiences.length }}
                experiencias registradas entre proyectos de Lima y Cusco.
              </p>
            </div>

            <div class="grid gap-3">
              <h3 class="font-semibold">Experiencia usada para este CV</h3>
              <div v-for="experience in workExperiences.slice(0, 2)" :key="experience.id" class="rounded-lg border border-border p-3 text-sm">
                <div class="flex flex-wrap items-center justify-between gap-2">
                  <strong>{{ experience.role }}</strong>
                  <Badge :variant="experience.status === 'Verificado' ? 'success' : 'default'">{{ experience.source }}</Badge>
                </div>
                <p class="mt-1 text-muted-foreground">{{ experience.project }} · {{ experience.period }}</p>
              </div>
            </div>

            <div class="flex flex-wrap gap-2">
              <Badge variant="outline">Kardex</Badge>
              <Badge variant="outline">Control de materiales</Badge>
              <Badge variant="outline">Seguridad en obra</Badge>
              <Badge variant="outline">Excel operativo</Badge>
            </div>
          </CardContent>
        </Card>
      </div>
    </section>

    <section v-else-if="activeView === 'certificates'" class="mx-auto grid max-w-7xl gap-6 px-5 py-7">
      <PageTitle eyebrow="Certificados" title="Tus constancias verificables" description="Comparte tus certificados con empresas y reclutadores." />
      <div class="grid gap-4 md:grid-cols-3">
        <Card v-for="course in courses.filter((item) => item.progress === 100 || item.status === 'Completado')" :key="course.id">
          <CardHeader>
            <Award class="h-5 w-5 text-teal-700" />
            <CardTitle>{{ course.title }}</CardTitle>
            <CardDescription>Emitido por Tukuy Academy · Código TA-2026-00{{ course.id.slice(-1) }}</CardDescription>
          </CardHeader>
          <CardContent>
            <Button variant="outline" class="w-full">Ver certificado</Button>
          </CardContent>
        </Card>
      </div>
    </section>

    <section v-else class="mx-auto grid max-w-7xl gap-6 px-5 py-7">
      <PageTitle eyebrow="Perfil" title="Tu información laboral" description="Mientras más completo esté tu perfil, mejores recomendaciones recibirás." />

      <div class="grid gap-5 lg:grid-cols-[380px_1fr]">
        <Card>
          <CardHeader class="items-center text-center">
            <Avatar class="h-20 w-20"><AvatarFallback class="text-xl">{{ user.initials }}</AvatarFallback></Avatar>
            <CardTitle>{{ user.name }}</CardTitle>
            <CardDescription>{{ user.trade }}</CardDescription>
          </CardHeader>
          <CardContent class="grid gap-4">
            <Progress :model-value="user.profileProgress" class="h-3" />
            <Button>Completar perfil laboral</Button>
          </CardContent>
        </Card>

        <Card>
          <CardHeader>
            <CardTitle>Datos principales</CardTitle>
            <CardDescription>Información visible para oportunidades laborales.</CardDescription>
          </CardHeader>
          <CardContent class="grid gap-3 text-sm md:grid-cols-2">
            <ProfileRow label="Oficio" :value="user.trade" />
            <ProfileRow label="Especialidad" :value="user.specialty" />
            <ProfileRow label="Ubicación" :value="user.location" />
            <ProfileRow label="Disponibilidad" value="Inmediata" />
            <ProfileRow label="Pretensión" value="S/ 1,800" />
            <ProfileRow label="Estado" value="Perfil verificado" />
          </CardContent>
        </Card>
      </div>

      <div class="grid gap-5 lg:grid-cols-[0.85fr_1.15fr]">
        <Card>
          <CardHeader>
            <Badge class="w-fit" variant="default">Completar perfil</Badge>
            <CardTitle>Importa o registra tu experiencia</CardTitle>
            <CardDescription>
              Si trabajaste usando Tukuy Obra o SIADEG, Academy puede simular la extracción de cargos, obras y módulos
              usados para alimentar tu CV.
            </CardDescription>
          </CardHeader>
          <CardContent class="grid gap-3">
            <button class="rounded-lg border border-border p-4 text-left transition hover:border-blue-200 hover:bg-blue-50" type="button">
              <div class="flex items-center justify-between gap-3">
                <strong>Importar desde Tukuy Obra / SIADEG</strong>
                <Badge variant="success">Recomendado</Badge>
              </div>
              <p class="mt-2 text-sm text-muted-foreground">
                Extrae obras donde participaste, cargo desempeñado, fechas, módulos utilizados y evidencias disponibles.
              </p>
            </button>

            <button class="rounded-lg border border-border p-4 text-left transition hover:border-blue-200 hover:bg-blue-50" type="button">
              <div class="flex items-center justify-between gap-3">
                <strong>Registrar experiencia manual</strong>
                <Badge variant="outline">Usuario</Badge>
              </div>
              <p class="mt-2 text-sm text-muted-foreground">
                Agrega experiencias que no estén conectadas al sistema para que también se consideren en tu CV y matching laboral.
              </p>
            </button>

            <div class="rounded-lg border border-teal-100 bg-teal-50 p-4 text-sm text-teal-900">
              Esta información mejora el CV inteligente y permite mostrar oportunidades laborales más precisas para la persona.
            </div>
          </CardContent>
        </Card>

        <Card>
          <CardHeader>
            <CardTitle>Experiencia laboral detectada</CardTitle>
            <CardDescription>Simulación de historial importado y declarado por el usuario.</CardDescription>
          </CardHeader>
          <CardContent class="grid gap-4">
            <div v-for="experience in workExperiences" :key="experience.id" class="rounded-lg border border-border p-4">
              <div class="flex flex-wrap items-start justify-between gap-3">
                <div>
                  <strong class="block">{{ experience.role }}</strong>
                  <span class="text-sm text-muted-foreground">{{ experience.project }} · {{ experience.location }}</span>
                </div>
                <Badge :variant="experience.status === 'Verificado' ? 'success' : experience.status === 'Declarado' ? 'warning' : 'default'">
                  {{ experience.status }}
                </Badge>
              </div>
              <p class="mt-3 text-sm text-muted-foreground">{{ experience.summary }}</p>
              <div class="mt-3 flex flex-wrap gap-2">
                <Badge variant="outline">{{ experience.source }}</Badge>
                <Badge variant="outline">{{ experience.period }}</Badge>
                <Badge v-for="module in experience.modules" :key="module" variant="outline">{{ module }}</Badge>
              </div>
            </div>
          </CardContent>
        </Card>
      </div>
    </section>

    <SiteFooter variant="light" />
  </main>
</template>
