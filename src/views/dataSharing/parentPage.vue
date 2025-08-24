<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

import childSubpagePage from '/src/views/dataSharing/dataSharingPage1.vue';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'parentPage',
});

const form = ref();
const lastName = ref();
const childSubpage = ref();

const formData = reactive({
  lastName: '',
});

function OnChildDataCaptured(e) {
  console.log(e);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Parent Page"

      prop="lastName"
    >
      <VueInput

        id="lastName"

        ref="lastName"
        v-model="formData.lastName"

        data-type="string"
      />
    </VueFormItem>

    <childSubpagePage

      id="childSubpage"
      ref="childSubpage"
      fst-name="Abhinav"

      :lst-name="formData.lastName"
      @on-child-emit="OnChildDataCaptured"
    />
  </VueForm>
</template>
