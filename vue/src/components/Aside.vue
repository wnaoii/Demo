<template>
    <div>
        <el-menu
                style="width: 200px; min-height: calc(100vh - 50px)"
                default-active="2"
                class="el-menu-vertical-demo">
        <el-sub-menu index="1">
            <template #title>
                <el-icon><location /></el-icon>
                <span>选项一</span>
            </template>
            <el-menu-item index="1-3">选项1-1</el-menu-item>
        </el-sub-menu>
        <el-menu-item index="2">
            <el-icon><icon-menu /></el-icon>
            <template #title>导航二</template>
        </el-menu-item>

        <el-menu-item index="4">
            <el-icon><setting /></el-icon>
            <template #title>导航三</template>
        </el-menu-item>
        </el-menu>
    </div>
</template>

<script>
    export default {
        name: "Aside"
    }
</script>

<style scoped>

</style>