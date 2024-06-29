<script setup>
  import {
    IconDownload,
  } from 'viy-ui';
  import {
    useI18n
  } from 'vue-i18n';
  import {
    useApi
  } from '@/composables/useApi';
  const {
    t
  } = useI18n();
  defineOptions({
    name: 'frontPagination',
  });
  const form = ref();
  const viy2Flex_D8sBU = ref();
  const viy2TableToolbar_HcgGV = ref();
  const viy2Flex_D8dui = ref();
  const viy2Table = ref();
  const viy2Pagination = ref();
  const formData = reactive({});
  const viy2TableToolbarRef = ref()
  const viy2TableEditConfig = reactive({
    trigger: 'click'
  });
  const viy2TableExportConfig = reactive({
    modes: ['current', 'selected', 'all'],
    mode: 'all',
    beforeExportMethod: ({
      options
    }) => {
      if (options.mode === 'all') {
        options.data = viy2Table.value.getTableData().fullData;
      }
    },
  });
  const viy2PaginationCurrentPage = ref(1);
  const viy2PaginationPageSize = ref(15)
  const tableDsApi = useApi({
    method: 'post',
    localData: (function() {
      var result = [];
      for (var i = 1; i <= 1000; i++) {
        result.push({
          id: i,
          name: ('Yamaha ' + i),
          type: i % 2,
          description: ('Description' + i)
        });
      }
      return result;
    })(),
  });
  const tableDs = tableDsApi.data;
  const viy2TablePageConfig = reactive({
    enabled: true,
    currentPage: viy2PaginationCurrentPage,
    pageSize: viy2PaginationPageSize,
    total: 0
  });
  const viy2TableIdEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'center',
      },
    };
  });
  const viy2TableNameEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'center',
      },
    };
  });
  const viy2TableTypeEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'center',
      },
    };
  });
  const viy2TableDescriptionEditRender = computed(() => {
    return {
      enabled: false,
      attrs: {
        textAlign: 'left',
      },
    };
  });
</script>
<template>
  <VueForm ref="form" :model="formData">
    <VueFlex direction="column" id="viy2Flex_D8sBU" ref="viy2Flex_D8sBU" class="full-height">
      <VueToolbar ref="viy2TableToolbarRef" :connect-table="viy2Table" :export="{icon: IconDownload}">
      </VueToolbar>
      <VueFlex direction="column" grow="1" id="viy2Flex_D8dui" ref="viy2Flex_D8dui">
        <VueTable :stripe="true" :border="true" height="100%" id="viy2Table" ref="viy2Table" :data="tableDs" :edit-config="viy2TableEditConfig" :export-config="viy2TableExportConfig" :page-config="viy2TablePageConfig">
          <VueInputColumn :edit-render="viy2TableIdEditRender" field="id" align="center" title="Id" header-align="center" min-width="100px">
          </VueInputColumn>
          <VueInputColumn :edit-render="viy2TableNameEditRender" field="name" align="center" :sortable="true" title="Name" header-align="center" min-width="200px" filter-type="content">
          </VueInputColumn>
          <VueInputColumn :edit-render="viy2TableTypeEditRender" field="type" align="center" title="Type" header-align="center" min-width="200px">
          </VueInputColumn>
          <VueInputColumn :edit-render="viy2TableDescriptionEditRender" field="description" align="left" title="Description" header-align="center" min-width="300px">
          </VueInputColumn>
        </VueTable>
      </VueFlex>
      <VuePagination id="viy2Pagination" ref="viy2Pagination" v-model:current-page="viy2PaginationCurrentPage" v-model:page-size="viy2PaginationPageSize" :total="viy2TablePageConfig.total">
      </VuePagination>
    </VueFlex>
  </VueForm>
</template>