<template>
  <n-form>
    <slot name="formHeader"></slot>
    <n-grid>
      <template v-for="schema in getSchema" :key="schema.field">

      </template>
    </n-grid>
  </n-form>
</template>
<script lang="ts" setup>
import { ref, unref, computed } from 'vue';
import { FormSchema, FormProps } from './types/form';
import { basicProps } from './props';
import FormItem from './components/FormItem.vue';

const props = defineProps(basicProps);

const schemaRef = ref<Nullable<FormSchema[]>>(null);
const propsRef = ref<Partial<FormProps>>({});
const getProps = computed((): FormProps => {
  return { ...props, ...unref(propsRef) } as FormProps;
});

const getSchema = computed((): FormSchema[] => {
  const schemas: FormSchema[] = unref(schemaRef) || (unref(getProps).schemas as any);
  for (const schema of schemas) {
    const { defaultValue } = schema;
    // handle date type
    // dateItemType.includes(component as string)
    if (defaultValue) {
      schema.defaultValue = defaultValue;
    }
  }
  return schemas as FormSchema[];
});
</script>