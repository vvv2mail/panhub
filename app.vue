<template>
  <div class="layout" data-v-5c746fb8>
    <!-- 背景装饰 -->
    <div class="bg-decoration" data-v-5c746fb8>
      <div class="blob blob-1" data-v-5c746fb8></div>
      <div class="blob blob-2" data-v-5c746fb8></div>
      <div class="blob blob-3" data-v-5c746fb8></div>
    </div>

    <!-- 顶部导航 -->
    <header class="header" data-v-5c746fb8>
      <nav class="nav" data-v-5c746fb8>
        <NuxtLink to="/" class="brand" data-v-5c746fb8>
          <span class="brand-icon" data-v-5c746fb8>🔍</span>
          <span class="brand-text" data-v-5c746fb8>PanHub</span>
        </NuxtLink>
        <div class="nav-actions" data-v-5c746fb8>
          <!-- GitHub 链接 -->
          <a
            href="https://github.com"
            target="_blank"
            rel="noopener noreferrer"
            class="btn-icon github-btn"
            data-v-5c746fb8
            aria-label="打开 GitHub 仓库"
            title="GitHub 仓库">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
            </svg>
          </a>
          <!-- 设置按钮 -->
          <button class="btn-icon" type="button" @click="openSettings = true" data-v-5c746fb8 aria-label="打开设置" title="设置">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="12" cy="12" r="3"></circle>
              <path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 0-2.83l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"></path>
            </svg>
          </button>
        </div>
      </nav>
    </header>

    <!-- 主内容区 -->
    <main class="main">
      <NuxtPage />
    </main>

    <!-- 设置抽屉 -->
    <ClientOnly>
      <SettingsDrawer
        v-model="settings"
        v-model:open="openSettings"
        :all-plugins="ALL_PLUGIN_NAMES"
        :all-tg-channels="allTgChannels"
        @save="saveSettings"
        @reset-default="resetToDefault" />
    </ClientOnly>

    <!-- Toast 通知 -->
    <div v-if="toast.show" class="toast" :class="toast.type" role="status" aria-live="polite">
      {{ toast.message }}
    </div>

    <!-- 密码门 -->
    <ClientOnly>
      <PasswordGate
        :show="showPasswordGate"
        :error="auth.error.value || ''"
        :submitting="unlockSubmitting"
        @unlock="onUnlock" />
    </ClientOnly>
  </div>
</template>

<script setup lang="ts">
import { ALL_PLUGIN_NAMES } from "./config/plugins";
import channelsConfig from "~/config/channels.json";

const { settings, loadSettings, saveSettings, resetToDefault } = useSettings();
const auth = useAuth();
const openSettings = ref(false);
const showPasswordGate = ref(false);
const unlockSubmitting = ref(false);
const pendingOnUnlock = ref<(() => void) | null>(null);

function requestUnlock(onSuccess?: () => void) {
  pendingOnUnlock.value = onSuccess ?? null;
  showPasswordGate.value = true;
}

async function onUnlock(password: string) {
  unlockSubmitting.value = true;
  const ok = await auth.unlock(password);
  unlockSubmitting.value = false;
  if (ok) {
    showPasswordGate.value = false;
    const cb = pendingOnUnlock.value;
    pendingOnUnlock.value = null;
    if (cb) {
      nextTick(() => cb());
    }
  }
}

provide("requestUnlock", requestUnlock);

// Toast 状态
const toast = ref({
  show: false,
  message: "",
  type: "info" as "info" | "success" | "error",
});

function showToast(message: string, type: "info" | "success" | "error" = "info") {
  toast.value = { show: true, message, type };
  setTimeout(() => {
    toast.value = false;
  }, 3000);
}

const allTgChannels = computed(() => {
  const configChannels = (useRuntimeConfig().public as any)?.tgDefaultChannels;
  return Array.isArray(configChannels) && configChannels.length > 0
    ? configChannels
    : channelsConfig.defaultChannels;
});

watch(() => settings.value, (newVal, oldVal) => {
  if (oldVal && newVal && JSON.stringify(newVal) !== JSON.stringify(oldVal)) {
    showToast("设置已保存", "success");
  }
}, { deep: true });

onMounted(() => {
  loadSettings();
  auth.fetchStatus();
});

provide('showToast', showToast);
</script>
<style scoped>
.layout {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  overflow-x: hidden;
  position: relative;
}

.bg-decoration {
  height: 100%;
  left: 0;
  overflow: hidden;
  pointer-events: none;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: -1;
}

.blob {
  animation: blobFloat 8s ease-in-out infinite;
  border-radius: 50%;
  filter: blur(48px);
  opacity: .28;
  position: absolute;
}

.blob-1 {
  animation-delay: 0s;
  background: linear-gradient(135deg,#0f766e,#14b8a6);
  height: 400px;
  left: -100px;
  top: -100px;
  width: 400px;
}

.blob-2 {
  animation-delay: 2s;
  background: linear-gradient(135deg,#f59e0b,#fb7185);
  bottom: -50px;
  height: 300px;
  right: -50px;
  width: 300px;
}

.blob-3 {
  animation-delay: 4s;
  background: linear-gradient(135deg,#0ea5e9,#14b8a6);
  height: 250px;
  left: 70%;
  top: 50%;
  width: 250px;
}

.header {
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  background: var(--bg-glass);
  border-bottom: 1px solid hsla(0,0%,100%,.3);
  box-shadow: var(--shadow-sm);
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav {
  gap: 16px;
  justify-content: space-between;
  margin: 0 auto;
  max-width: 1100px;
  padding: 16px 24px;
}

.brand, .nav {
  align-items: center;
  display: flex;
}

.brand {
  color: var(--text-primary);
  font-size: 20px;
  font-weight: 700;
  gap: 8px;
  text-decoration: none;
  transition: transform var(--transition-fast);
}

.brand:hover {
  transform: scale(1.05);
}

.brand-icon {
  filter: drop-shadow(0 2px 4px rgba(15,118,110,.3));
  font-size: 24px;
}

.brand-text {
  background: linear-gradient(135deg,var(--primary),var(--secondary));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-actions {
  gap: 8px;
}

.btn-icon, .nav-actions {
  align-items: center;
  display: flex;
}

.btn-icon {
  -webkit-backdrop-filter: blur(10px);
  backdrop-filter: blur(10px);
  background: #ffffff80;
  border: 1px solid hsla(0,0%,100%,.3);
  border-radius: var(--radius-md);
  color: var(--text-primary);
}
</style>

