<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { get } from 'lodash-es';
import { useApi } from '@/composables/useApi';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'form_Designer',
});

const form = ref();
const printName = ref();
const fstName = ref();
const lstName = ref();
const apiText = ref();
const apiTextDisplay = ref();
const viy2Dropdown_OZwTL = ref();
const gender = ref();
const setBtn = ref();
const clickButton = ref();

const formData = reactive({
  FirstName: '', LastName: '', apiText: '', apiTextDisplay: '', gender: '',
});

const apiTextDisplayProps = computed(() => {
    	return {
    label: 'location.street.name',
    value: 'name.first',

  };
});

const genderOpts = reactive([
  { value: 'Option 1', label: 'Option 1' },
  { value: 'Option 2', label: 'Option 2' },
  { value: 'Option 3', label: 'Option 3' },
]);

const apiCallingDataSetApi = useApi({
  url: 'https://randomuser.me/{id}',
  method: 'get',
  pathParams: {
    id: 'api',
  },
  responseType: 'json',

}, {
  onSuccess: (data, params) => {
  // do something
    console.log('Successfully fetched the data.....');
  },
  onError:
(e, params) => {
  // do something
  console.log('Failed to fetch data');
},
});
const apiCallingDataSet = apiCallingDataSetApi.data;
const fetchDataListApi = useApi({
  url: 'https://randomuser.me/api/',
  method: 'get',
  responseType: 'json',

});
const fetchDataList = fetchDataListApi.data;

const apiTextBlur = (event) => {
  // do some thing
  console.log('You blurred me.....');
  console.log(event);
};

const setBtnClick = () => {
  setButtonData();
};
const clickButtonClick = () => {
  // do some thing
  printFormData();
}

;

function printFormData() {
  console.log(formData.FirstName);
  console.log(formData.LastName);
  console.log(formData.apiTextDisplay);
}

function setButtonData() {
  formData.FirstName = 'Abhinav';
  formData.LastName = 'Maheshwari';
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueButton id="printName" ref="printName" icon-position="left" size="default" :link="true" :text="true" color="#EE00FF">
      Click
    </VueButton>

    <VueFormItem

      :label="t('label.FirstName')"

      prop="FirstName"
    >
      <VueInput

        id="fstName"

        ref="fstName"
        v-model="formData.FirstName"

        data-type="string"
      />
    </VueFormItem>

    <VueFormItem

      :label="t('label.LastName')"

      prop="LastName"
    >
      <VueInput

        id="lstName"

        ref="lstName"
        v-model="formData.LastName"

        data-type="string"
      />
    </VueFormItem>

    <VueFormItem

      label="Api Text"

      prop="apiText"
    >
      <VueInput
        id="apiText"

        ref="apiText"

        v-model="formData.apiText"
        type="textarea"

        placeholder="Below is the fetched data"

        @blur="apiTextBlur"
      />
    </VueFormItem>

    <VueFormItem

      label="Api Text Display"

      prop="apiTextDisplay"
    >
      <VueSelect

        id="apiTextDisplay"
        ref="apiTextDisplay"

        v-model="formData.apiTextDisplay"

        :options="get(apiCallingDataSet, 'results')"

        :props="apiTextDisplayProps"
      />
    </VueFormItem>

    <VueDropdown

      id="viy2Dropdown_OZwTL"

      ref="viy2Dropdown_OZwTL"
      :split-button="true"
    >
      <VueIcon class="vue-icon--left" />
      Dropdown
      <template #dropdown>
        <VueDropdownMenu />
      </template>
    </VueDropdown>

    <VueFormItem

      label="Gender "

      prop="gender"
    >
      <VueRadioGroup

        id="gender"

        ref="gender"
        v-model="formData.gender"

        direction="horizontal"

        split-size="default"
      >
        <VueRadio
          v-for="option in genderOpts"
          :key="option.value"
          :label="option.value"
        >
          {{ option.label }}
        </VueRadio>
      </VueRadioGroup>
    </VueFormItem>

    <VueButton id="setBtn" ref="setBtn" icon-position="left" @click="setBtnClick">
      Set
    </VueButton>
    <VueButton id="clickButton" ref="clickButton" icon-position="left" @click="clickButtonClick">
      Click
    </VueButton>
  </VueForm>
</template>
