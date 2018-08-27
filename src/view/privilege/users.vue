<template>
  <div class="user-list">
    <div >
      <Layout>
        <Sider>
          <Card>
            <p slot="title">组织架构</p>
            <template>
              <Tree :data="data1"></Tree>
            </template>
          </Card>
        </Sider>
        <Layout>
          <Content>
            <Card>
              <i-button type="primary" icon="ios-add" >添加</i-button>
              <Icon type="chevron-left"></Icon>
              <i-button type="primary" icon="ios-add">修改</i-button>
              <i-button type="warning" icon="ios-delete"><Icon type="android-delete"></Icon>删除</i-button>

              <BaseList
                ref="tables"
                searchable
                searchKey="keyword"
                search-place="top"
                v-model="tableData"
                :columns="columns"
                @on-delete="handleDelete"
              />

            </Card>
          </Content>
        </Layout>
      </Layout>
    </div>

  </div>
</template>

<script>
import Tables from '_c/tables'
import BaseList from '_c/base-list'
import { getTableData } from '@/api/data'
export default {
  name: 'system',
  components: {
    Tables,
    BaseList
  },
  data () {
    return {
      columns: [
        {title: '姓名', key: 'name', sortable: true},
        {title: '工号', key: 'userNo', editable: true},
        {title: '公司', key: 'company', editable: true},
        {title: '部门', key: 'department', editable: true},
        {title: '角色', key: 'roles', editable: true},
        {title: '手机', key: 'mobile', editable: true},
        {title: '邮箱', key: 'email', editable: true},
        {title: '备注', key: 'remark'},
        {
          title: '操作',
          key: 'handle',
          options: ['delete'],
          button: [
            (h, params, vm) => {
              return h('Poptip', {
                props: {
                  confirm: true,
                  title: '你确定要删除吗?'
                },
                on: {
                  'on-ok': () => {
                    vm.$emit('on-delete', params)
                    vm.$emit('input', params.tableData.filter((item, index) => index !== params.row.initRowIndex))
                  }
                }
              })
            }
          ]
        }
      ],
      tableData: [],
      data1: [
        {
          title: '亚厦股份',
          expand: true,
          children: [
            {
              title: '亚厦装饰',
              expand: true,
              children: [
                {
                  title: '信息部'
                },
                {
                  title: '技术开发部'
                }
              ]
            },
            {
              title: '亚厦蘑菇加',
              expand: true,
              children: [
                {
                  title: '平台中心'
                },
                {
                  title: '产品规划部'
                }
              ]
            }
          ]
        }
      ]
    }
  },
  methods: {
    handleDelete (params) {
      console.log(params)
    }
  },
  mounted () {
    getTableData().then(res => {
      this.tableData = res.data
    })
  }
}
</script>

<style>
.user-list .ivu-layout-sider, .user-list .ivu-layout-header{
  background:white;
}
</style>
