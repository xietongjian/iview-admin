<template>
  <div>
    <Card>
      <Button type="primary" @click="modal1 = true" icon="ios-add">添加</Button>
      <Modal
        v-model="modal1"
        title="添加"
        @on-ok="ok"
        @on-cancel="cancel">
        <Form ref="formValidate" :model="formValidate" :rules="ruleValidate" :label-width="80">
          <FormItem label="系统名称" prop="name">
            <Input v-model="formValidate.name" placeholder="请输入系统名称！"></Input>
          </FormItem>
          <FormItem label="系统标识" prop="sn">
            <Input v-model="formValidate.sn" placeholder="请输入系统标识！"></Input>
          </FormItem>
          <FormItem label="URL" prop="url">
            <Input v-model="formValidate.url" placeholder="请输入系统URL！"></Input>
          </FormItem>
          <FormItem label="描述" prop="desc">
            <Input v-model="formValidate.desc" type="textarea" :autosize="{minRows: 2,maxRows: 5}" placeholder="请输入系统描述！"></Input>
          </FormItem>
        </Form>
      </Modal>
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
      modal1: false,
      formValidate: {
        name: '',
        sn: '',
        url: '',
        desc: ''
      },
      ruleValidate: {
        name: [
          { required: true, message: '系统名称不能为空', trigger: 'blur' }
        ],
        sn: [
          { required: true, message: '系统标识不能为空', trigger: 'blur' }
        ],
        url: [
          { required: true, message: '系统URL不能为空', trigger: 'blur' },
          { type: 'url', message: '请输入正确的URL', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    handleDelete (params) {
      console.log(params)
    },
    ok () {
      //this.handleSubmit('formValidate')
        // this.$Message.info('Clicked ok');
    },
    cancel () {
      this.$Message.info('Clicked cancel');
    },
    handleSubmit (name) {
      this.$refs[name].validate((valid) => {
        if (valid) {
          this.$Message.success('Success!');
        } else {
          this.$Message.error('Fail!');
        }
      })
    },
    handleReset (name) {
      this.$refs[name].resetFields();
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
