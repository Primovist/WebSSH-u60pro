<template>
  <el-container class="manage-container">
    <el-main>
      <div>
        <el-tabs v-model="data.active_name" type="card">
          <Connect></Connect>
          <Account></Account>
          <NetFilter></NetFilter>
          <LoginAudit></LoginAudit>
          <SshdUser></SshdUser>
          <SshdCert></SshdCert>
        </el-tabs>
      </div>
    </el-main>
  </el-container>
</template>

<script setup lang="ts">
import { reactive } from "vue";
import { useRouter } from "vue-router";
import { useGlobalStore } from "@/stores/store";
import Account from "@/components/Account.vue";
import Connect from "@/components/Connect.vue";
import NetFilter from "@/components/NetFilter.vue";
import LoginAudit from "@/components/LoginAudit.vue";
import SshdUser from "@/components/SshdUser.vue";
import SshdCert from "@/components/SshdCert.vue";

let router = useRouter();
let globalStore = useGlobalStore();

let data = reactive({
  active_name: "connectInfo",
});

/**
 * 回到主页
 */
function goHome() {
  router.push({ name: "Home" })
}

/**
 * 退出登陆
 */
function logout() {
  globalStore.logout();
  router.push({ "name": "Login" });
}

</script>

<style scoped>
.manage-container {
  width: 100%;
  min-width: 0;
  background-color: #fff;
}

.manage-container :deep(.el-main) {
  min-width: 0;
}

.manage-container :deep(.management-toolbar-scroll),
.manage-container :deep(.management-table-scroll) {
  display: block;
  width: 100%;
  min-width: 0;
  overflow-x: auto;
  overflow-y: hidden;
  -webkit-overflow-scrolling: touch;
}

.manage-container :deep(.management-toolbar) {
  display: flex;
  width: max-content;
  min-width: 100%;
  align-items: center;
  gap: 18px;
  white-space: nowrap;
}

.manage-container :deep(.management-toolbar .toolbar-item) {
  flex: 0 0 auto;
}

.manage-container :deep(.management-toolbar .toolbar-search) {
  width: 400px;
}

.manage-container :deep(.management-toolbar .toolbar-input) {
  width: 220px;
}

.manage-container :deep(.management-toolbar .el-form-item) {
  margin-bottom: 0;
  flex-wrap: nowrap;
}

.manage-container :deep(.management-table) {
  width: 100%;
  min-width: 940px;
}

.manage-container :deep(.management-table.audit-table) {
  min-width: 1560px;
}

.manage-container :deep(.management-table .cell),
.manage-container :deep(.management-table th.el-table__cell),
.manage-container :deep(.management-table td.el-table__cell) {
  white-space: nowrap;
}

.manage-container :deep(.table-actions) {
  display: inline-flex;
  flex-wrap: nowrap;
  align-items: center;
  gap: 8px;
  white-space: nowrap;
}

.manage-container :deep(.table-actions .el-button + .el-button) {
  margin-left: 0;
}

@media (max-width: 768px) {
  .manage-container :deep(.el-main) {
    padding: 0;
  }

  .manage-container :deep(.el-tabs__nav-wrap) {
    padding: 0 !important;
    overflow-x: auto !important;
    overflow-y: hidden;
    scrollbar-width: none;
    -webkit-overflow-scrolling: touch;
    touch-action: pan-x;
  }

  .manage-container :deep(.el-tabs__nav-wrap::-webkit-scrollbar) {
    display: none;
  }

  .manage-container :deep(.el-tabs__nav-scroll) {
    overflow: visible !important;
    width: max-content;
    min-width: 100%;
  }

  .manage-container :deep(.el-tabs__nav) {
    display: flex;
    width: max-content;
    float: none;
    transform: none !important;
    white-space: nowrap;
  }

  .manage-container :deep(.el-tabs__item) {
    flex: 0 0 auto;
    box-sizing: border-box;
    padding-inline: 14px;
  }

  .manage-container :deep(.el-tabs__nav-prev),
  .manage-container :deep(.el-tabs__nav-next) {
    display: none;
  }
}
</style>
