<template>
<div>
        <r-header :title="title" :showBack="showBack" :backText="this.$t('common.back')"></r-header>
        <r-actionsheet :model="showMenu" value="status" :menuList="menuList" :headerHtml="headerHtml" :onClick="onClickSheet"/>
</div>
</template>

<script>
import i18n from '../i18n/index';

export default {

  props: {
    title: String,
    showBack: Boolean
  },
  data() {
    return {
      showMenu: {},
      menuList: {
          'zh-CN': '中文',
          'en-US': 'English'
      }
    };
  },
  methods: {
    onClickMore() {
        this.showMenu.status = !this.showMenu.status;
    },
    onClickSheet(key) {
      i18n.locale = key;
    }
  },
  computed: {
    headerHtml() {
        return `<h6>${this.$t('common.language')}</h6>`;
    }
  }
};
</script>