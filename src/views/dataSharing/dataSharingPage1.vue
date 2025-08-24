<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

// child props are written here
const props = defineProps(['fstName', 'lstName']);
const emit = defineEmits(['onChildEmit']);
const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'dataSharingPage1',
});

const form = ref();
const FirstName = ref();
const childParent = ref();
const childButton = ref();

const formData = reactive({
  FirstName: '',
});

const childParentClick = () => {
  sendValueToParent();
};
const childButtonClick = () => {
  // do some thing
  getValueFromParent();
}

;

function getValueFromParent() {
  // console.log(fstName);
  console.log(props.lstName);
}

function sendValueToParent() {
  emit('onChildEmit', formData.FirstName);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueFormItem

      label="Child Page"

      prop="FirstName"
    >
      <VueInput

        id="FirstName"

        ref="FirstName"
        v-model="formData.FirstName"

        data-type="string"
      />
    </VueFormItem>

    <VueButton id="childParent" ref="childParent" icon-position="left" @click="childParentClick">
      Emit Value to Parent
    </VueButton>
    <VueButton id="childButton" ref="childButton" icon-position="left" @click="childButtonClick">
      Get Value from parent
    </VueButton>
  </VueForm>
</template>
