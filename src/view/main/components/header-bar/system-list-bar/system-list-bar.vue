<template>
  <div class="system-list-box">
    <!--<Breadcrumb :style="{fontSize: `${fontSize}px`}">
      <BreadcrumbItem v-for="item in list" :to="item.to" :key="`bread-crumb-${item.name}`">
        <common-icon style="margin-right: 4px;" :type="item.icon || ''"/>
        {{ showTitle(item) }}
      </BreadcrumbItem>
    </Breadcrumb>-->

    <Tabs type="line" >
      <TabPane label="权限系统" icon="logo-apple"></TabPane>
      <TabPane label="考勤系统" icon="logo-windows"></TabPane>
      <TabPane label="MDM" icon="logo-tux"></TabPane>
      <TabPane label="门户系统" icon="logo-tux"></TabPane>
      <TabPane label="财务系统" icon="logo-tux"></TabPane>
      <TabPane label="工程管理系统" icon="logo-tux"></TabPane>
      <TabPane label="项目管理系统" icon="logo-tux"></TabPane>
      <TabPane label="CMS" icon="logo-tux"></TabPane>
      <TabPane label="订单管理" icon="logo-tux"></TabPane>
    </Tabs>
  </div>
</template>
<script>
import { showTitle } from '_c/common/util'
import CommonIcon from '_c/common-icon'
import './system-list-bar.less'
export default {
  name: 'systemListBar',
  components: {
    CommonIcon
  },
  props: {
    list: {
      type: Array,
      default: () => []
    },
    fontSize: {
      type: Number,
      default: 14
    },
    showIcon: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    showTitle (item) {
      return showTitle(item, this)
    },
    isCustomIcon (iconName) {
      return iconName.indexOf('_') === 0
    },
    getCustomIconName (iconName) {
      return iconName.slice(1)
    }
  }
}
</script>
