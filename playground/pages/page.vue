<template>
  <div>
    <p>{{ $t('key1.key1.key1.key1.key1') }}</p>
    <i18n-t
      keypath="key1.key1.key1.key1.key1"
      tag="h1"
    >
      <template #default="{ translation }">
        <strong>{{ translation.replace('page', 'page replace') }}</strong> <i>!!!</i>
      </template>
    </i18n-t>

    <i18n-t keypath="feedback.text">
      <template #link>
        <nuxt-link :to="{ name: 'index' }">
          <i18n-t keypath="feedback.link" />
        </nuxt-link>
      </template>
    </i18n-t>

    <p>Current Locale: {{ $getLocale() }}</p>

    <div>
      {{ $t('welcome', { username: 'Alice', unreadCount: 5 }) }}
    </div>
    <div>
      {{ $tc('apples', 10) }}
    </div>

    <!-- Formatted number and date examples -->
    <div>
      Formatted Number: {{ $tn(1234567.89) }}
    </div>
    <div>
      Formatted Date: {{ $td('2023-12-31') }}
    </div>

    <!-- Ссылки для переключения локалей -->
    <div>
      <button
        v-for="locale in $getLocales()"
        :key="locale"
        :disabled="locale === $getLocale()"
        @click="$switchLocale(locale.code)"
      >
        Switch to {{ locale.code }}
      </button>
    </div>

    <div>
      <NuxtLink :to="$localeRoute({ name: 'index' })">
        Go to Index
      </NuxtLink>
      |
      <NuxtLink :to="$localeRoute({ name: 'subpage' })">
        Go to subpage
      </NuxtLink>
      |
      <NuxtLink :to="$localeRoute({ name: 'subpage' }, 'en')">
        Go to subpage en
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
import { useNuxtApp } from '#imports'

const { $getLocale, $switchLocale, $getLocales, $localeRoute, $t, $tc, $tn, $td } = useNuxtApp()
</script>
