<script setup lang="ts">
import { ref } from "vue";

const name = ref("");
const email = ref("");
const phone = ref("");
const message = ref("");
const status = ref<"idle" | "sending" | "success" | "error">("idle");

const submitForm = async () => {
  status.value = "sending";

  try {
    await new Promise((resolve) => setTimeout(resolve, 1000));
    status.value = "success";
    name.value = "";
    email.value = "";
    phone.value = "";
    message.value = "";
  } catch {
    status.value = "error";
  }
};
</script>

<template>
  <section id="contacto" class="bg-slate-50 px-6 py-24" aria-labelledby="contact-title">
    <div class="mx-auto max-w-2xl">
      <div class="mb-12 text-center">
        <span class="mb-3 block text-xs font-medium uppercase tracking-[0.2em] text-brand">
          Contáctanos
        </span>
        <h2 id="contact-title" class="font-display text-3xl font-semibold text-primary sm:text-4xl">
          ¿Hablamos?
        </h2>
        <p class="mt-4 text-lg leading-relaxed text-slate-500">
          Cuéntanos qué necesitas y estudiaremos cómo podemos ayudarte.
        </p>
      </div>

      <div
        v-if="status === 'success'"
        id="form-status"
        class="rounded-xl border border-green-200 bg-green-50 p-12 text-center"
        role="status"
      >
        <div class="mx-auto mb-5 flex size-14 items-center justify-center rounded-full bg-green-100 text-2xl text-green-600" aria-hidden="true">✓</div>
        <h3 class="font-display text-xl font-semibold text-slate-800">¡Mensaje preparado!</h3>
        <p class="mt-2 text-slate-500">La demostración del formulario se ha completado correctamente.</p>
      </div>

      <form
        v-else
        class="space-y-6 rounded-xl border border-slate-100 bg-white p-8 shadow-sm md:p-10"
        @submit.prevent="submitForm"
        aria-describedby="form-status"
      >
        <div class="grid gap-6 sm:grid-cols-2">
          <div>
            <label for="name" class="mb-2 block text-sm font-medium text-slate-700">Nombre completo</label>
            <input id="name" v-model="name" required type="text" name="name" autocomplete="name" placeholder="María García" class="w-full rounded-lg border border-slate-200 px-4 py-3 text-sm text-slate-800 outline-none transition-colors placeholder:text-slate-400 focus:border-brand focus:ring-2 focus:ring-brand/30" />
          </div>
          <div>
            <label for="email" class="mb-2 block text-sm font-medium text-slate-700">Correo electrónico</label>
            <input id="email" v-model="email" required type="email" name="email" autocomplete="email" placeholder="maria@ejemplo.com" class="w-full rounded-lg border border-slate-200 px-4 py-3 text-sm text-slate-800 outline-none transition-colors placeholder:text-slate-400 focus:border-brand focus:ring-2 focus:ring-brand/30" />
          </div>
        </div>

        <div>
          <label for="phone" class="mb-2 block text-sm font-medium text-slate-700">Teléfono <span class="font-normal text-slate-400">(opcional)</span></label>
          <input id="phone" v-model="phone" type="tel" name="phone" autocomplete="tel" placeholder="+34 600 000 000" class="w-full rounded-lg border border-slate-200 px-4 py-3 text-sm text-slate-800 outline-none transition-colors placeholder:text-slate-400 focus:border-brand focus:ring-2 focus:ring-brand/30" />
        </div>

        <div>
          <label for="message" class="mb-2 block text-sm font-medium text-slate-700">Mensaje</label>
          <textarea id="message" v-model="message" required rows="5" name="message" placeholder="Cuéntanos qué necesitas..." class="w-full resize-none rounded-lg border border-slate-200 px-4 py-3 text-sm text-slate-800 outline-none transition-colors placeholder:text-slate-400 focus:border-brand focus:ring-2 focus:ring-brand/30"></textarea>
        </div>

        <p v-if="status === 'error'" id="form-status" class="text-sm text-red-600" role="alert">
          Ha ocurrido un error. Inténtalo nuevamente.
        </p>

        <button :disabled="status === 'sending'" :aria-busy="status === 'sending'" type="submit" class="w-full rounded-lg bg-brand px-6 py-3.5 font-semibold text-white transition-colors hover:bg-blue-700 disabled:cursor-not-allowed disabled:opacity-60">
          {{ status === "sending" ? "Enviando..." : "Enviar mensaje" }}
        </button>
      </form>
    </div>
  </section>
</template>
