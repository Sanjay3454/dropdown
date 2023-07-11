<script>
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const restList = ref([]);

const getData = async () => {
  try {
    const response = await fetch('/db.json');
    const data = await response.json();
    console.log(data.products);
    restList.value = data.products.map(list=>list);
    console.log(restList.value)
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};




    onMounted(() => {
      getData();
    });

    return {
      restList
    };
  }
};






  
</script>

<template>

  <div class="container">
    <div class="select-container">
      <select name="cars" id="cars">
        <option v-for="product in restList" :key="product.id" :value="product.name">{{ product.name }}</option>
      </select>
      <select name="options1" id="options1">
        <template v-for="product in restList">
          <option v-if="product.offer && product.offer.list1" v-for="item in product.offer.list1" :key="item" :value="item">{{ item }}</option>
        </template>
      </select>
      <select name="options2" id="options2">
        <template v-for="product in restList">
          <option v-if="product.offer && product.offer.list2" v-for="item in product.offer.list2" :key="item" :value="item">{{ item }}</option>
        </template>
      </select>
    </div>
  </div>
</template>


<style>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.category-button {
    padding: 10px 20px;
    font-size: 16px;
     background-color: #85fc6e;
    border: none;
    outline: none;
    cursor: pointer;
    margin-top: -36rem;
    margin-left: -58rem;
}
.select-container {
  display: flex;
  align-items: center;
  gap: 10px;
}

select {
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.container{
     color:Black;
    margin-left: -39rem;
    margin-top: -32rem;

}

</style>