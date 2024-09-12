<template>
    <div class="wraper">
        二维码已过期，请重新生成！
    </div>
</template>

<script setup>
import { ElMessage } from 'element-plus'
function getQueryParams(url) {
  const urlObj = new URL(url);
  const searchParams = urlObj.searchParams;
  const queryParams = {};

  for (const [key, value] of searchParams.entries()) {
    queryParams[key] = value;
  }

  return queryParams;
}
async function judgeExpiringQrCode() {
    const { expires, qrCodeUrl } = getQueryParams(window.location.href);
    // console.log(1111, expires, qrCodeUrl )
    const expireTime = new Date(Number(expires));
    const nowTime = new Date();
    if(expireTime < nowTime) {
        ElMessage({
            message: '二维码已过期，请重新生成！',
            type: 'warning',
        })
        return;
    }
    window.location.href = qrCodeUrl;
}
judgeExpiringQrCode();
</script>
<style>
.wraper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100vw;
    height: 100vh;
}
</style>
