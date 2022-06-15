<template>
    <div class="base-table">
        <el-table
        :data="tableData"
        :stripe="stripe"
        :border="border"
        :row-class-name="rowClassName"
        :span-method="spanMethod"
        >
        <base-column v-bind="$attrs"
            v-for="(item, index) in tableColumn"
            :key="index"
            :column="item">
        </base-column>
        </el-table>
        <el-pagination
            v-if="pagination"
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page.sync="currentPage"
            :page-sizes="pageSizes"
            :total="total"
            layout="total, prev, pager, next"
            class="base-table-pagination"
            :style="{ 'margin-top': paginationTop, 'text-align': paginationAlign }">
        </el-pagination>
    </div>
</template>

<script>
import BaseColumn from './base-column.vue'

export default {
    name: 'BaseElTable',
    components: { BaseColumn },
    props: {
        tableColumn: Array,
        tableData: Array,
        stripe: Boolean,
        border: Boolean,
        rowClassName: Function,
        spanMethod: Function,
        pagination: Boolean,
        currentPage: {
            type: Number,
            default: 0
        },
        pageSizes: {
            type: Array,
            default: () => [5, 10, 20, 50]
        },
        total: {
            type: Number,
            default: 0
        },
        paginationTop: {
            type: String,
            default: '20px'
        },
        paginationAlign: {
            type: String,
            default: 'center'
        }
    },

    methods: {
        handleSizeChange(val) {
            this.$emit('size-change', val)
        },

        handleCurrentChange(val) {
            this.$emit('current-change', val)
        },


    }
}
</script>