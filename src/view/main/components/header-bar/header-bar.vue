<template>
  <div class="header-bar">
    <Layout style="overflow:hidden;height:60px;">
      <Sider width="50" >
        <sider-trigger :collapsed="collapsed" icon="md-menu" @on-change="handleCollpasedChange"></sider-trigger>
      </Sider>
      <Content>
        <Layout>
          <Content>
            <system-list-bar show-icon style="width:100%;" :list="breadCrumbList"></system-list-bar>
          </Content>
          <Sider >
            <div class="custom-content-con">
              <slot></slot>
            </div>
          </Sider>
        </Layout>
      </Content>
    </Layout>

    <!--<custom-bread-crumb show-icon style="margin-left: 30px;" :list="breadCrumbList"></custom-bread-crumb>-->



  </div>
</template>
<script>
import siderTrigger from './sider-trigger'
import customBreadCrumb from './custom-bread-crumb'
import systemListBar from './system-list-bar'
import './header-bar.less'
export default {
  name: 'HeaderBar',
  components: {
    siderTrigger,
    customBreadCrumb,
    systemListBar
  },
  props: {
    collapsed: Boolean
  },
  computed: {
    breadCrumbList () {
      return this.$store.state.app.breadCrumbList
    }
  },
  methods: {
    handleCollpasedChange (state) {
      this.$emit('on-coll-change', state)
    }
  }
}
</script>
