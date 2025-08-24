<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

import childPage2Page from '/src/views/dataSharing/child2.vue';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

const defaultName = ref('Hii this is the default name');

defineOptions({
  name: 'parent2',
});

const form = ref();
const parentInput = ref();
const childPage2 = ref();

const formData = reactive({
  parentInput: '',
});

function emptyUserFirstName(e) {
  formData.parentInput = '';
}

function displaySelectedText(val) {
  console.log(val);
  defaultName.value = val;
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Parent Input"

      prop="parentInput"
    >
      <VueInput

        id="parentInput"

        ref="parentInput"
        v-model="formData.parentInput"

        data-type="string"
      />
    </VueFormItem>

    <VueText id="displayName" ref="displayName" :style="{ width: '100%', display: 'inline-block' }" v-html="defaultName" />
    <childPage2Page

      id="childPage2"
      ref="childPage2"
      :fst-name="formData.parentInput"

      @blank-first-name="emptyUserFirstName"
      @select-first-name="displaySelectedText"
    />
  </VueForm>
</template>
