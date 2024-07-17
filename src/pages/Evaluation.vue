<template>
  <div class="page-container">
    <div v-if="currentState == 'pre'" class="pre-container">
      <el-result icon="success" title="数据采集成功!" sub-title="点击“开始评估”">
        <template #extra>
          <el-button color="#4b4d75" dark size="large" @click="onEvaluationButtonClick">开始评估</el-button>
        </template>
      </el-result>
    </div>
    <div v-if="currentState == 'ing'" class="ing-container">
      <el-result title="评估中..." sub-title="数据正在评估中，请稍后...">
        <template #icon>
          <el-icon size="large" class="is-loading">
            <Loading />
          </el-icon>
        </template>
      </el-result>
    </div>
    <div v-if="currentState == 'result'" class="result-container">
      <el-row :gutter="20">
        <el-col :span="4">
        </el-col>
        <el-col :span="16">
          <el-card>
            <template #header>
              <div class="card-header">
                <span>评估结果明细</span>
              </div>
            </template>

            <el-descriptions class="margin-top" :column="3" :border="true">
              <el-descriptions-item>
                <template #label>
                  <div class="cell-item">
                    样本编号
                  </div>
                </template>
                NO.000001
              </el-descriptions-item>
              <el-descriptions-item>
                <template #label>
                  <div class="cell-item">
                    样本大小
                  </div>
                </template>
                180MB
              </el-descriptions-item>
              <el-descriptions-item>
                <template #label>
                  <div class="cell-item">
                    样本模式
                  </div>
                </template>
                EEG & NIRS
              </el-descriptions-item>
              <el-descriptions-item :span="3">
                <template #label>
                  <div class="cell-item">
                    2D结果可视化
                  </div>
                </template>
                <el-image :src="VisualizationResult2D" lazy />
              </el-descriptions-item>
              <el-descriptions-item :span="3">
                <template #label>
                  <div class="cell-item">
                    3D结果可视化
                  </div>
                </template>
                <el-image :src="VisualizationResult3D" lazy />
              </el-descriptions-item>
            </el-descriptions>

            <template #footer>
              <el-button color="#4b4d75" dark size="large" style="width: 100%;" @click="onRetryButtonClick">结果有疑义，我要“重新评估”</el-button>
            </template>
          </el-card>
        </el-col>
        <el-col :span="4">
        </el-col>
      </el-row>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from 'vue';
import VisualizationResult2D from '../assets/2D-visualization-result.png';
import VisualizationResult3D from '../assets/3D-visualization-result.png';

const emit = defineEmits(['retry-evaluation']);
const currentState = ref<'pre' | 'ing' | 'result'>('pre');

const onEvaluationButtonClick = () => {
  currentState.value = 'ing';

  setTimeout(() => {
    currentState.value = 'result';
  }, 2_000);
};

const onRetryButtonClick = () => {
  emit('retry-evaluation');
};
</script>
<style scoped>
.page-container {
  width: 100%;
  height: 100%;

  overflow: scroll;
}

.result-container {
  padding-top: 50px;
  padding-bottom: 200px;
}

.pre-container, .ing-container {
  height: 100%;

  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>