<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

import parentPopUpPopupComp from '/src/views/dataSharing/popUpChild.vue';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'popUpParent',
});

const form = ref();
const parentPopUp = ref();

const formData = reactive({
  parentPopUp: '',
});

const parentPopUpSelect = (selectedObj) => {
  // do something
  console.log(selectedObj);
  formData.parentPopUp = `${selectedObj.firstName} ${selectedObj.lastName}`;
}

;
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Category"

      prop="parentPopUp"
    >
      <VueValueList

        id="parentPopUp"

        ref="parentPopUp"

        v-model="formData.parentPopUp"

        popup-type="dialog"

        aside-direction="rtl"
        dialog-width="500"

        :use-popup="true"

        :popup-component="parentPopUpPopupComp"

        @select="parentPopUpSelect"
      />
    </VueFormItem>
  </VueForm>
</template>
