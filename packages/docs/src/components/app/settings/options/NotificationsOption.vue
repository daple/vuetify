<template>
  <v-defaults-provider
    :defaults="{
      VIcon: {
        color: user.notifications.show ? 'primary' : 'disabled'
      }
    }"
  >
    <settings-switch
      v-model="user.notifications.show"
      :label="t('enable-notifications')"
      :messages="t('enable-notifications-message')"
    >
      <template #append>
        <v-btn
          :color="isDisabled ? undefined : 'primary'"
          :disabled="isDisabled"
          :text="t('reset')"
          size="small"
          variant="outlined"
          @click="onResetNotifications"
        />
      </template>
    </settings-switch>
  </v-defaults-provider>
</template>

<script setup>
  // Composables
  import { useI18n } from 'vue-i18n'

  // Stores
  import { useUserStore } from '@vuetify/one'

  // Utilities
  import { computed } from 'vue'

  const { t } = useI18n()
  const user = useUserStore()

  const isDisabled = computed(() => user.notifications.read.length === 0)

  function onResetNotifications () {
    user.notifications.read = []
  }
</script>
