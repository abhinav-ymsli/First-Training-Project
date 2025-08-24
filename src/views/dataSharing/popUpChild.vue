<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';
import { useApi } from '@/composables/useApi';

const emitValue = defineEmits(['select']);
const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

defineOptions({
  name: 'popUpChild',
});

const form = ref();
const nameTable = ref();
const setValue = ref();

const formData = reactive({
});

const nameTableEditConfig = reactive({
  trigger: 'click',

});

const nameTableMouseConfig = reactive({

  extension: true,

});

const nameTableRowConfig = reactive({
  isCurrent: true,
});

const TableDataListApi = useApi({
  method: 'post',
  localData: [
    { firstName: 'Abhinav', lastName: 'Maheshwari' },
    { firstName: 'Saumayy', lastName: 'Aggarwal' },
  ],

});
const TableDataList = TableDataListApi.data;

const nameTableFirstNameEditRender = computed(() => {
  return {
    enabled: false,
  };
});

const nameTableLastNameEditRender = computed(() => {
  return {
    enabled: false,
  };
});

const setValueClick = () => {
  setSelected();
};

function setSelected() {
  // alert("this is selected")
  const fetchRecord = nameTable.value.getCurrentRecord();
  console.log(fetchRecord);
  alert(`${fetchRecord.firstName} ${fetchRecord.lastName}`);
  emitValue('select', fetchRecord);
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueTable

      id="nameTable"

      ref="nameTable"

      :stripe="true"

      :border="true"
      :show-header="true"

      :data="TableDataList"

      :edit-config="nameTableEditConfig"
      :mouse-config="nameTableMouseConfig"
      :row-config="nameTableRowConfig"
    >
      <VueInputColumn

        :edit-render="nameTableFirstNameEditRender"

        field="firstName"

        title="First Name"

        width="300px"
      />
      <VueInputColumn

        :edit-render="nameTableLastNameEditRender"

        field="lastName"

        width="500px"

        title="Last Name"
      />
    </VueTable>

    <VueButton id="setValue" ref="setValue" icon-position="left" @click="setValueClick">
      set Value
    </VueButton>
  </VueForm>
</template>
