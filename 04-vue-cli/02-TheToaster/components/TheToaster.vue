<template>
  <div class="toasts">
    <ui-toast v-for="(toast, index) in toasts" :id="toast.id" :key="index" :type="toast.type">{{
      toast.message
    }}</ui-toast>
  </div>
</template>

<script>
import UiToast from './UiToast';
import { nanoid } from 'nanoid';

export default {
  name: 'TheToaster',
  components: { UiToast },
  data() {
    return {
      id: 0,
      toasts: [],
      timeout: 5000,
    };
  },
  methods: {
    success(message) {
      let toastId = nanoid();
      this.toasts.push({
        id: toastId,
        type: 'success',
        message: message,
      });
      this.setDeleteToastTimer(toastId);
    },
    error(message) {
      const toastId = nanoid();
      this.toasts.push({
        id: toastId,
        type: 'error',
        message: message,
      });
      this.setDeleteToastTimer(toastId);
    },
    setDeleteToastTimer(toastId) {
      setTimeout(() => {
        this.toasts = this.toasts.filter((i) => i.id !== toastId);
      }, this.timeout);
    },
  },
};
</script>

<style scoped>
.toasts {
  position: fixed;
  bottom: 8px;
  right: 8px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  white-space: pre-wrap;
  z-index: 999;
}

@media all and (min-width: 992px) {
  .toasts {
    bottom: 72px;
    right: 112px;
  }
}
</style>
