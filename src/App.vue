<template>
  <div id="app">
    <h1>SMT上板看板</h1>
    <div class="data-input">
      <textarea v-model="jsonInput" placeholder="请输入JSON数据" rows="5" cols="50"></textarea>
      <button @click="parseJson">解析数据</button>
    </div>
    <div v-if="data.length > 0" class="data-display">
      <h2>数据展示</h2>
      <table>
        <thead>
          <tr>
            <th>工单号</th>
            <th>物料号</th>
            <th>上板SN</th>
            <th>完成进度</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in data" :key="index">
            <td>{{ item.workOrder }}</td>
            <td>{{ item.materialNumber }}</td>
            <td>{{ item.serialNumber }}</td>
            <td>{{ item.progress }}%</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const jsonInput = ref('');
    const data = ref([]);

    const parseJson = () => {
      try {
        const parsedData = JSON.parse(jsonInput.value);
        if (Array.isArray(parsedData)) {
          data.value = parsedData;
        } else {
          alert('请输入有效的JSON数组');
        }
      } catch (error) {
        alert('JSON解析错误，请检查输入');
      }
    };

    return {
      jsonInput,
      data,
      parseJson,
    };
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 20px;
  background-color: #f4f4f4;
}

#app {
  max-width: 800px;
  margin: 0 auto;
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
  color: #2c3e50;
}

.data-input {
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  background: #3498db;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1em;
  transition: background 0.3s;
}

button:hover {
  background: #2980b9;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>