<template>
    <div class="page-container">
        <div class="control-container" v-loading="connectLoading" element-loading-text="正在连接中...">
            <div class="page-title">连接设备 和 测试连接设备</div>
            <div class="button-group">
                <el-row :gutter="20">
                    <el-col :span="12">
                        <el-button type="primary" size="large" plain color="#8889ac" style="width: 100%;" @click="connect">开始连接设备</el-button>
                    </el-col>
                    <el-col :span="12">
                        <el-button type="primary" size="large" plain color="#8889ac" style="width: 100%;">测试设备</el-button>
                    </el-col>
                </el-row>
            </div>
        </div>
    </div>
</template>
<script setup lang="ts">
import { ref } from "vue";

const connectLoading = ref(false);
const emit = defineEmits(['connect-success']);

const connect = () => {
    connectLoading.value = true;

    setTimeout(() => {
        emit('connect-success');
    }, 2_400);
};

</script>
<style scoped>
.page-container {
    width: 80%;
    height: 80%;

    background-color: #8889ac;

    position: absolute;
    top: 45%;
    left: 50%;
    transform: translate(-50%, -48%);
}

.control-container {
    width: 90%;
    height: 90%;

    background-image: url('../assets/connect-control-background.jpg'); /* 背景图片的路径 */
    background-size: cover; /* 让背景图片覆盖整个 div */
    background-position: center; /* 将背景图片居中显示 */
    background-repeat: no-repeat; /* 禁止背景图片重复 */

    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);

    position: absolute;
    top: 54%;
    left: 50%;
    transform: translate(-50%, -42%);
}

.page-title {
    color: #FFFFFF;
    font-size: 36px;

    position: absolute;

    top: -60px;
}

.button-group {
    width: 500px;
    height: 40px;
    position: absolute;
    bottom: 80px;
    right: 20px;
}
</style>