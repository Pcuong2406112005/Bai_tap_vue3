<script setup>
import { ref,watch,onMounted } from 'vue'
const currentscreen=ref('dshocsinh');
const falculties = ref([
  {
    tennganh: 'CNTT',
    caclop: [
      { lop: 'CN01', students: [{ name: 'Phan Mạnh Cường', age: 20 }] },
      { lop: 'CN02', students: [{ name: 'Lê Doãn Kiên Trung', age: 20 }] }
    ]
  },
  {
    tennganh: 'CNDPT',
    caclop: [
      { lop: 'PT01', students: [{ name: 'Nguyễn Tuấn Dũng', age: 20 }] },
      { lop: 'PT02', students: [{ name: 'Lê Quốc Dũng', age: 20 }] }
    ]
  }
]);
const chonChucNang=(chonthem)=>{
  if(chonthem==='themnganh') {
    currentscreen.value='themnganh';
  }
  else{
    currentscreen.value='themlop';
  }
};
const xoanganh=(index)=>{
  falculties.value.splice(index,1);
};
const xoalop=(index,index1)=>{
  falculties.value[index].caclop.splice(index1,1);
}
const tenlopmoi=ref('');
const nganhchon=ref('');
const luulop=()=>{
  if(tenlopmoi.value&&nganhchon.value){
    const falculty=falculties.value.find(x=>x.tennganh===nganhchon.value);
    if(falculty){
      falculty.caclop.push({lop:tenlopmoi.value,students:[]});
      tenlopmoi.value='';
      nganhchon.value='';
      chonThem.value='';
      currentscreen.value='dslop';
    }
    else{
      alert('Hãy điền đủ thông tin');
    }
  }
  else{
      alert('Hãy điền đủ thông tin');
    }
};
const chonThem=ref('');
const tennganhmoi=ref('');
const themnganh=()=>{
  if(tennganhmoi.value){
    falculties.value.push({tennganh:tennganhmoi.value,caclop:[]});
    tennganhmoi.value='';
    chonThem.value='';
    currentscreen.value='dslop';
  }
  else{
      alert('Hãy điền đủ thông tin');
    }
}
const editLopIndex=ref({nganhIndex:null,lopIndex:null});
const sualop=ref('');
const startEditLop=(nganhIndex,lopIndex)=>{
  editLopIndex.value={nganhIndex,lopIndex};
  sualop.value=falculties.value[nganhIndex].caclop[lopIndex].lop;
};
const saveEditLop=()=>{
  const {nganhIndex,lopIndex} =editLopIndex.value;
  falculties.value[nganhIndex].caclop[lopIndex].lop=sualop.value;
  editLopIndex.value={nganhIndex:null,lopIndex:null};
  sualop.value='';
};
const editNganhIndex=ref(null);
const tennganhSua=ref('');
const startEditNganh=(index)=>{
  editNganhIndex.value=index;
  tennganhSua.value=falculties.value[index].tennganh;
}
const saveEditNganh=()=>{
  falculties.value[editNganhIndex.value].tennganh=tennganhSua.value;
  editNganhIndex.value=null;
  tennganhSua.value='';
};
const xoahocsinh=(index,index1,index2)=>{
  falculties.value[index].caclop[index1].students.splice(index2,1);
}
const TEN=ref('');
const TUOI=ref(null);
const themhocsinh=()=>{
  currentscreen.value='addhs';
}
const loP=ref('');
const LuuHocSinh = () => {
  const ten = TEN.value;
  const tuoi = TUOI.value;
  for (const nganh of falculties.value) {
    for (const lop of nganh.caclop) {
      if (lop.lop === loP.value) {
        lop.students.push({ name: ten, age: Number(tuoi) });
      }
    }
  }
  TEN.value = '';
  TUOI.value = null;
  loP.value = '';
  currentscreen.value = 'dshocsinh';
};
const editing = ref({
  nganh: null,
  lop: null,
  hs: null,
  name: '',
  age: null
});
const batdausua = (nganhIndex, lopIndex, hsIndex) => {
  const student = falculties.value[nganhIndex].caclop[lopIndex].students[hsIndex];
  editing.value = {
    nganh: nganhIndex,
    lop: lopIndex,
    hs: hsIndex,
    name: student.name,
    age: student.age
  };
};

const luusausua = () => {
  const e = editing.value;
  const hs = falculties.value[e.nganh].caclop[e.lop].students[e.hs];
  hs.name = e.name;
  hs.age = e.age;
  editing.value = { nganh: null, lop: null, hs: null, name: '', age: null };
};


const dangsua = (i, j, k) => {
  const e = editing.value;
  return e.nganh === i && e.lop === j && e.hs === k;
};
watch(falculties, (newVal) => {
  localStorage.setItem('falculties', JSON.stringify(newVal));
}, { deep: true });
onMounted(() => {
  const data = localStorage.getItem('falculties');
  if (data) {
    falculties.value = JSON.parse(data);
  }
});


</script>

<template>
<div v-if="currentscreen==='addhs'">
 <select @change="chonLop(loP)" v-model="loP">
  <option disabled value="">--Chọn Lớp</option>
  <template v-for="(nganh,index) in falculties" :key="index">
    <option disabled value="">{{ nganh.tennganh }}</option>
    <template v-for="(CacLop,index1) in nganh.caclop" :key="index1">
      <option :value="CacLop.lop">{{ CacLop.lop }}</option>
    </template>
  </template>
 </select><br>
 Tên Học Sinh:<input v-model="TEN"><br>
 Tuổi:<input v-model="TUOI"><br>
 <button @click="LuuHocSinh">Lưu Học Sinh</button>
</div>
 <div v-if="currentscreen==='dshocsinh'">
  <button @click="themhocsinh">Thêm Học Sinh</button>
  <table border="1">
    <thead>
      <tr>
      <th>STT</th>
      <th>Họ và Tên</th>
      <th>Tuổi</th>
      <th>Lớp</th>
      <th>Thao Tác</th>
      </tr>
    </thead>
    <tbody>
      <template v-for="(nganh,index) in falculties" :key="index">
        <template v-for="(Caclop,index1) in nganh.caclop" :key="index1">
          <template v-for="(hocsinh,index2) in Caclop.students" :key="index2">
            <tr>
              <td>{{ (index+1)+'.'+(index1+1)+'.'+(index2+1) }}</td>
              <td>
                <template v-if="dangsua(index,index1,index2)">
                  <input v-model="editing.name">
                </template>
                <template v-else>
                  {{ hocsinh.name }}
                </template>
              </td>
              <td>
                <template v-if="dangsua(index,index1,index2)">
                  <input v-model="editing.age" >
                </template>
                <template v-else>
                  {{ hocsinh.age }}
                </template>
              </td>
              <td>{{ Caclop.lop }}</td>
              <td>
                <template v-if="dangsua(index,index1,index2)">
                  <button @click="luusausua">Lưu</button>
                </template>
                <template v-else>
                  <button @click="batdausua(index,index1,index2)">Chỉnh Sửa</button>
                  <button @click="xoahocsinh(index,index1,index2)">Xóa</button>
                </template>
              </td>
            </tr>
          </template>
        </template>
      </template>
    </tbody>
  </table>
  <button @click="currentscreen='dslop'">DSLớp</button>
 </div>
<div v-if="currentscreen==='dslop'">  
  <div>
  <select @change="chonChucNang(chonThem)" v-model="chonThem">
    <option disabled value="">--Chọn Chức Năng--</option>
    <option value="themlop">Thêm lớp</option>
    <option value="themnganh">Thêm ngành</option>
  </select>
  </div>
  <table border="1" cellpadding="8">
    <thead>
      <tr>
        <th>STT</th>
        <th>Lớp</th>
        <th>Thao Tác</th>
      </tr>
    </thead>
    <tbody>
      <template v-for="(nganh,index) in falculties" :key="index">
        <tr>
          <td>{{ index+1 }}</td>
          <td>
            <template v-if="editNganhIndex===index">
              <input v-model="tennganhSua"/>
              <button @click="saveEditNganh">Lưu</button>
            </template>
            <template v-else>
              {{ nganh.tennganh }}
            </template>
          </td>
          <td>
            <button @click="xoanganh(index)">Xóa Ngành</button>
            <button @click="startEditNganh(index)">Sửa ngành</button>
          </td>
        </tr>

        <tr v-for="(lop,index1) in nganh.caclop" :key="`${index}-${index1}`">
          <td>{{ (index+1)+'.'+(index1+1) }}</td>
          <td>
            <template v-if="editLopIndex.nganhIndex===index&&editLopIndex.lopIndex===index1">
              <input v-model="sualop">
              <button @click="saveEditLop">Lưu</button>
            </template>
            <template v-else>{{ lop.lop }}</template>
          </td>
          <td>
            <button @click="xoalop(index,index1)">Xóa lớp</button>
            <button @click="startEditLop(index,index1)">Chỉnh Sửa</button>
          </td>
        </tr>
      </template>
    </tbody>
  </table>
  <button @click="currentscreen='dshocsinh'">DS Học Sinh</button>
</div>
<div v-if="currentscreen==='themlop'">
  Tên Lớp:<input v-model="tenlopmoi"><br>
  Thuộc ngành:<select v-model="nganhchon">
    <option disabled>--Chọn Ngành--</option>
    <option v-for="nganh in falculties" :key="nganh.tennganh" :value="nganh.tennganh">{{ nganh.tennganh }}</option>
  </select><br>
  <button @click="luulop">Lưu</button>
</div>
<div v-if="currentscreen==='themnganh'">
  Tên ngành:<input v-model="tennganhmoi"><br>
  <button @click="themnganh">Thêm ngành</button>
</div>
</template>
