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

@media (max-width: 768px) {
  .manage-container :deep(.el-main) {
    padding: 0;
  }

  .manage-container :deep(.el-tabs__nav-wrap) {
    overflow-x: auto;
    scrollbar-width: none;
    -webkit-overflow-scrolling: touch;
  }

  .manage-container :deep(.el-tabs__nav-wrap::-webkit-scrollbar) {
    display: none;
  }

  .manage-container :deep(.el-tabs__nav-scroll) {
    width: max-content;
    min-width: 100%;
  }

  .manage-container :deep(.el-tabs__nav) {
    float: none;
    white-space: nowrap;
  }

  .manage-container :deep(.el-tabs__item) {
    padding-inline: 14px;
  }
}
</style>
