<template>
  <div>
    <p>{{ $t('key1.key1.key1.key1.key1') }}</p>
    <p>Current Locale: {{ $getLocale() }}</p>

    <!-- Ссылки для переключения локалей -->
    <div>
      <button
        v-for="locale in $getLocales()"
        :key="locale.code"
        :disabled="locale.code === $getLocale()"
        @click="$switchLocale(locale.code)"
      >
        Switch to {{ locale.code }}
      </button>
    </div>

    <p id="localized-route">
      {{ $localeRoute({ name: 'page' }, 'de').path }}
    </p>

    <div>
      <i18n-link :to="{ name: 'page' }">
        Go to Page
      </i18n-link>
    </div>

    <a href="/">test</a>

    <div>
      <i18n-switcher
        :custom-labels="{ en: 'English', de: 'Deutsch', ru: 'Русский' }"
      />
    </div>

    <div
      v-for="key in generatedKeys"
      :key="key"
    >
      <p>{{ key }}: <span v-if="$has(key)">{{ $t(key) }}</span></p>
    </div>
  </div>
</template>

<script setup>
// Function to generate keys with a fixed pattern
function generateKeys(depth, maxKeys = 4) {
  const keys = []

  const generate = (prefix = '', currentDepth = depth) => {
    if (currentDepth === 0) {
      for (let i = 0; i <= maxKeys; i++) {
        // Генерируем ключ с инкрементом по последнему элементу
        keys.push(`${prefix}key${i}`)
      }
      return
    }

    for (let i = 0; i <= maxKeys; i++) {
      // Добавляем к префиксу текущий элемент
      generate(`${prefix}key${i}.`, currentDepth - 1)
    }
  }

  generate()
  return keys
}

const generatedKeys = ref(generateKeys(4))
</script>
