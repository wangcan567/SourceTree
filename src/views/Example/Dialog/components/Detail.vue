<script setup lang="ts">
import { PropType } from 'vue'
import type { TableData } from '@/api/table/types'
import { Descriptions } from '@/components/Descriptions'
import { useI18n } from '@/hooks/web/useI18n'
import { ElTag } from 'element-plus'

const { t } = useI18n()

defineProps({
  currentRow: {
    type: Object as PropType<Nullable<TableData>>,
    default: () => null
  },
  detailSchema: {
    type: Array as PropType<DescriptionsSchema[]>,
    default: () => []
  }
})
</script>

<template>
  <Descriptions :schema="detailSchema" :data="currentRow || {}">
    <template #importance="{ row }: { row: TableData }">
      <ElTag :type="row.importance === 1 ? 'success' : row.importance === 2 ? 'warning' : 'danger'">
        {{
          row.importance === 3
            ? t('exampleDemo.important')
            : row.importance === 2
            ? t('exampleDemo.good')
            : t('exampleDemo.commonly')
        }}
      </ElTag>
    </template>

    <template #content="{ row }: { row: TableData }">
      <div v-html="row.content"></div>
    </template>
  </Descriptions>
</template>
