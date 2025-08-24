<script setup>
import { useLockScreen } from 'viy-ui';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const lockScreenUtils = useLockScreen();
const lockScreen = lockScreenUtils.lockScreen;

const router = useRouter();

defineOptions({
  name: 'navigationPage',
});

const form = ref();
const navigateDetail = ref();
const openTag = ref();

const formData = reactive({
});

const navigateDetailClick = () => {
  navigateToDetail();
};
const openTagClick = () => {
  openTagManually();
};

function navigateToDetail() {
  router.push('detailPage');
}

function openTagManually() {
  useMultiTags().openTag({
    name: 'detailpage',
  });
}
</script>

<template>
  <VueForm ref="form" v-loading="lockScreen" :model="formData">
    <VueButton id="navigateDetail" ref="navigateDetail" icon-position="left" @click="navigateDetailClick">
      Navigate To Detail
    </VueButton>
    <VueButton id="openTag" ref="openTag" icon-position="left" @click="openTagClick">
      open Tag Manually
    </VueButton>
  </VueForm>
</template>
