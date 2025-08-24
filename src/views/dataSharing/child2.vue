<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const props = defineProps(['fstName']);
const emitValue = defineEmits(['blankFirstName', 'selectFirstName']);
const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

const nameList = ref([]);
defineOptions({
  name: 'child2',
});

const form = ref();
const addList = ref();
const nameDropDown = ref();

const formData = reactive({
  nameDropDown: '',
});

const nameDropDownProps = computed(() => {
    	return {
    label: 'fstName',
    value: 'fstName',

  };
});

const addListClick = () => {
  addToList();
};
const nameDropDownChange = (val, option, oldVal, oldOption) => {
  // do some thing
  emitValue('selectFirstName', val);
};

function addToList() {
  // pushing the elements to the array
  nameList.value.push({ fstName: props.fstName });
  emitValue('blankFirstName');
  // formData.parentInput = '';
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueButton id="addList" ref="addList" icon-position="left" @click="addListClick">
      Add To List
    </VueButton>

    <VueFormItem

      label="Name List"

      prop="nameDropDown"
    >
      <VueSelect

        id="nameDropDown"
        ref="nameDropDown"

        v-model="formData.nameDropDown"

        :options="nameList"

        :props="nameDropDownProps"

        @change="nameDropDownChange"
      />
    </VueFormItem>
  </VueForm>
</template>
