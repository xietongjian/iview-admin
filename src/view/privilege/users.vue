<template>
  <div>
    <div >
      <Layout>
        <Sider>
          <template>
            <Tree :data="data1"></Tree>
          </template>
        </Sider>
        <Layout>
          <Header>Header</Header>
          <Content>
            <Card>
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
        {title: '系统图标', key: 'name', sortable: true},
        {title: '系统名称', key: 'email', editable: true},
        {title: '系统标识', key: 'sn', editable: true},
        {title: 'URL前缀', key: 'url', editable: true},
        {title: '排序号', key: 'sortNo', editable: true},
        {title: '备注', key: 'remark', editable: true},
        {title: '创建时间', key: 'createTime'},
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
          title: 'parent 1',
          expand: true,
          children: [
            {
              title: 'parent 1-1',
              expand: true,
              children: [
                {
                  title: 'leaf 1-1-1'
                },
                {
                  title: 'leaf 1-1-2'
                }
              ]
            },
            {
              title: 'parent 1-2',
              expand: true,
              children: [
                {
                  title: 'leaf 1-2-1'
                },
                {
                  title: 'leaf 1-2-1'
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

</style>
