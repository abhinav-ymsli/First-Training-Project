<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'demo_page',
});

const form = ref();
const viy2Button_6ygOAY = ref();

const formData = reactive({
});
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueButton id="viy2Button_6ygOAY" ref="viy2Button_6ygOAY" icon-position="left">
      Button
    </VueButton>
  </VueForm>
</template>
