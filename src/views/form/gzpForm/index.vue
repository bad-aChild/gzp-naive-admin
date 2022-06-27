<template>
  <div>
      <BasicForm :schemas="schemas">
        <template #formHeader>
          <div>头部</div>
        </template>
      </BasicForm>
  </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import { BasicForm } from '@/components/baseFrom/index'
const schemas = [{
    field: 'field1',
    component: 'Input',
    label: '字段1',
    colProps: {
      span: 8,
    },
    // componentProps:{},
    // can func
    componentProps: ({ schema, formModel }) => {
      console.log('form:', schema);
      console.log('formModel:', formModel);
      return {
        placeholder: '自定义placeholder',
        onChange: (e: any) => {
          console.log(e);
        },
      };
    },
    renderComponentContent: () => {
      return {
        prefix: () => '',
        suffix: () => 'sSlot',
      };
    },
  },]
</script>