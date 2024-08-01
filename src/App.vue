<template>
  <div class="container mt-3">
    <h1 class="fs-4 mb-4 text-center">2024 Vue 前端新手營 - Composition API - 第一週</h1>
    <table class="table align-middle">
      <thead>
        <tr>
          <th class="w-25">品項</th>
          <th class="w-25">描述</th>
          <th class="">價格</th>
          <th>庫存</th>
          <th>編輯</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in menuData" :key="item.id">
          <td>{{ item.name }}</td>
          <td>
            <small>{{ item.description }}</small>
          </td>
          <td>{{ item.price }}</td>
          <td>
            <div class="d-flex align-items-center">
              <button
                type="button"
                class="btn btn-outline-primary btn-sm"
                @click="decreaseStock(item)"
                :class="{ disabled: item.stock < 1 }"
              >
                -
              </button>
              <p class="mx-3 my-0" style="width: 20px">{{ item.stock }}</p>
              <button
                type="button"
                class="btn btn-outline-primary btn-sm"
                @click="increaseStock(item)"
              >
                +
              </button>
            </div>
          </td>
          <td>
            <button type="button" class="btn btn-danger btn-sm" @click="editItem(item)">
              編輯
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="editingItem">
      <h5>編輯品項</h5>
      <label for="name" class="col-form-label">品項</label>
      <input class="form-control w-25 me-3" v-model="editingItem.name" />
      <label for="description" class="col-form-label">描述</label>
      <input class="form-control w-25 me-3" v-model="editingItem.description" />
      <label for="price" class="col-form-label">價格</label>
      <input class="form-control w-25 me-3" v-model.number="editingItem.price" />
      <div class="mt-3">
        <button type="button" class="btn btn-primary me-3" @click="confirmEdit">確認</button>
        <button type="button" class="btn btn-outline-secondary" @click="cancelEdit">取消</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 菜單資料
const menuData = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])

// 編輯中的品項
const editingItem = ref(null)

//  減少庫存
const decreaseStock = (item) => {
  if (item.stock > 0) {
    item.stock--
  }
}

// 增加庫存
const increaseStock = (item) => {
  item.stock++
}

// 編輯品項
const editItem = (item) => {
  editingItem.value = { ...item }
}

// 確認編輯
const confirmEdit = () => {
  // 找出編輯中的品項
  const item = menuData.value.find((i) => i.id === editingItem.value.id)
  // 更新品項資料
  if (item) {
    item.name = editingItem.value.name
    item.description = editingItem.value.description
    item.price = editingItem.value.price
  }
  editingItem.value = null
}

// 取消編輯
const cancelEdit = () => {
  editingItem.value = null
}
</script>
