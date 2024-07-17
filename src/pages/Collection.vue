<template>
  <div class="page-container">
    <div class="section-title">
      <h5>EGG 模式 & NIRS 模式</h5>
      <h2 class="title">一键多模式采集</h2>
    </div>
    <div class="input-container">
      <el-row :gutter="20">
        <el-col :span="6">
        </el-col>
        <el-col :span="12">
          <el-input placeholder="用户信息输入" size="large" />
        </el-col>
        <el-col :span="6">
        </el-col>
      </el-row>
    </div>
    <div class="select-container">
      <el-row :gutter="20">
        <el-col :span="4">
        </el-col>
        <el-col :span="16">
          <el-row :gutter="20">
            <el-col :span="12">
              <el-card style="height: 300px;">
                <div class="mode-title">
                  <el-avatar :size="50" :src="'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png'" />
                  <h4>EEG 模式</h4>
                  <div style="flex-grow: 1;"></div>
                  <el-checkbox label="选择" size="large" :border="true" />
                </div>
                <div class="mode-descript">
                  <span>
                    EEG（事件相关电位）模式主要通过脑电图（EEG）来记录大脑活动，通常用于研究认知过程、情绪反应等。EGG模式的数据处理包括数据预处理、滤波、去噪以及特征提取等步骤，最终进行统计分析和模型评估。
                  </span>
                </div>
              </el-card>
            </el-col>
            <el-col :span="12">
              <el-card style="height: 300px;">
                <div class="mode-title">
                  <el-avatar :size="50" :src="'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png'" />
                  <h4>NIRS 模式</h4>
                  <div style="flex-grow: 1;"></div>
                  <el-checkbox label="选择" size="large" :border="true" />
                </div>
                <div class="mode-descript">
                  <span>
                    NIRS（近红外脑成像）模式则利用近红外光谱技术来监测脑部血氧变化，从而推断脑功能状态。NIRS模式的数据处理流程较为复杂，包括数据准备、质量检查、预处理、个体水平分析、组水平统计和结果可视化等多个步骤。具体来说，使用NIRS_SPM进行激活分析时，需要对原始数据进行格式转化、使用定位信息创建MNI空间坐标、滤波、一阶建模、GLM模型评估、设置设计矩阵、计算beta值等。
                  </span>
                </div>
              </el-card>
            </el-col>
          </el-row>
        </el-col>
        <el-col :span="4">
        </el-col>
      </el-row>
    </div>
    <div class="action-container">
      <el-row :gutter="20">
        <el-col :span="8">
        </el-col>
        <el-col :span="8">
          <el-button color="#4b4d75" dark size="large" style="width: 100%;" @click="onCollectButtonClick">开始采集</el-button>
        </el-col>
        <el-col :span="8">
        </el-col>
      </el-row>
    </div>

    <el-dialog
      v-model="isCollecting"
      title="采集中..."
      width="500"
      :close-on-click-modal="false"
      :close-on-press-escape="false"
      :show-close="false"
    >
      <div
        v-loading="isCollecting"
        element-loading-text="正在采集中，请稍后..."
        style="height: 160px;"
      ></div>
    </el-dialog>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits(['collect-success']);
const isCollecting = ref(false);

const onCollectButtonClick = () => {
  isCollecting.value = true;

  setTimeout(() => {
    isCollecting.value = false;
    emit('collect-success');
  }, 3_000);
};

</script>
<style scoped>
.page-container {
  width: 100%;
  height: 100%;
}

.section-title {
  width: 100%;
  text-align: center;
  padding-top: 30px;
  padding-bottom: 30px;
}

.input-container {
  padding-top: 30px;
  padding-bottom: 30px;
}

.section-title h5 {
  font-weight: 500;
  display: block;
  text-transform: uppercase;
  font-size: 14px;
  line-height: 27px;
  margin-bottom: 4px;
  margin-top: 7px;
  position: relative;
  font-family: 'IBM Plex Sans', sans-serif;
  color: #8889ac;
}

.section-title h2.title {
  color: #4b4d75;
  font-size: 39px;
  line-height: 48px;
  margin-bottom: 10px;
}

.select-container {
  width: 100%;

  padding-top: 30px;
  padding-bottom: 30px;
}

.mode-title {
  color: #4b4d75;

  display: flex;
  align-items: center;
}

.mode-title h4 {
  margin-left: 15px;
}

.mode-descript {
  color: #8889ac;
  font-size: 14px;
  line-height: 27px;
}

.action-container {
  width: 100%;

  padding-top: 30px;
  padding-bottom: 30px;
}
</style>