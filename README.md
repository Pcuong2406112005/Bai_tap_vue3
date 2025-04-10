<template>

<div class="thanhtimkiem">
  <input type="search" v-model.number="search" placeholder="Tìm Kiếm"/> 
</div>
<table border="1">
  <thead>
    <tr>
      <th>STT</th>
      <th>Họ Tên</th>
      <th>Tuổi</th>
      <th>Lớp</th>
      <th>Thao Tác</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(student,index) in students" :key="index">
      <td>{{ index+1 }}</td>
      <td>{{ student.name }}</td>
      <td>{{ student.age }}</td>
      <td>{{ student.lop }}</td>
      <td>Chỉnh sửa/Xóa</td>
    </tr>
  </tbody>
</table>
<div v-if="findstudent">
  <p><strong>Học Sinh được tìm thấy:</strong></p>
  <p>Họ Tên:{{ findstudent.name }}</p>
  <p>Tuổi:{{ findstudent.age }}</p>
  <p>Lớp:{{ findstudent.lop }}</p>
</div>
<div v-else>
  <p>Không tìm thấy học sinh tương ứng với STT.</p>
</div>
</template>
<style scoped>
.thanhtimkiem{
  display:flex;
  justify-content:center;
  align-items: center;
}
</style>
<script setup>
import { ref,computed } from 'vue';
const search=ref('');
const students = ref([
  { name: 'Phan Mạnh Cường', age: 20, lop: 'CN03' },
  { name: 'Nguyễn Văn A', age: 21, lop: 'CN02' },
  { name: 'Trần Thị B', age: 19, lop: 'CN01' },
]);
const findstudent=computed(() => {
  if(search.value>=1&&search.value<=students.value.length){
    return students.value[search.value-1];
  }
  return null;
}
);
</script>
