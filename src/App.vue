<template>
  <div class="container mt-20">
    <!-- 1) sử dụng v-if và v-show để ẩn hiện thể p khi ấn vào nút Switch-->
    <div class="exercise">
      <div class="row">
        <div class="col-sm-4">
          <b-button variant="danger" class="mb-20" @click="onSwitch">Switch</b-button>
        </div>
        <div class="col-sm-4">
          <p v-if="isDisplayPTag">Show/Hide</p>
        </div>
        <div class="col-sm-4">
          <p v-show="isDisplayPTag">Show/Hide</p>
        </div>
      </div>
    </div>
    <!-- end of exercise 1 -->

    <!-- 2) In ra 1 list li , kèm theo index. Ấn vào Add sẽ add 1 phần tử vào  
					Nếu index chẵn thì background của li màu xanh
					Nếu index lẻ thì background của li màu đỏ
					scope style
    -->
    <div class="exercise">
      <div class="row">
        <div class="col-sm-4">
          <b-button size="lg" variant="primary" class="mb-20" @click="onAddingItem">Add</b-button>
        </div>
        <div class="col-sm-8">
          <ul>
            <li v-for="(item, index) in listItems" :key="index" :class="setColor(index)">{{index}}</li>
          </ul>
        </div>
      </div>
    </div>
    <!-- end of exercise 2 -->

    <!-- Exercis 3 -->
    <div class="exercise">
      <div class="row">
        <!-- 3) In ra 1 list array những object gồm key, value, index. 
            Hiện text số chẵn nếu value chẵn và lẻ đối với value lẻ
            ví dụ array có dạng array: [{a:1,b:2}, {x:2,y:4}]
            kết quả là: 
            <li> a -index 0 số lẻ</li>
            <li> b -index 1 số chẵn</li>
            <li> x -index 0 số chẵn</li>
            <li> y -index 1 số chẵn</li>
        -->
        <ul>
          <hr>
          <li>{{listObjects}}</li>
          <hr>
          <li v-for="(object, index) in listObjects" :key="index">
            <p
              v-for="(value, key, index) in object"
              :key="index"
            >{{value}} -index {{index}} {{isOddorEven(value)}}</p>
          </li>
        </ul>
      </div>
    </div>
    <!-- Exercise 4 -->
    <div class="exercise">
      <div class="row">
        <input type="number" v-model="inputNumber">&nbsp;
        <b-button variant="success" class="mb-20" @click="Increase()">Increase</b-button>&nbsp;
        <b-button variant="warning" class="mb-20" @click="Decrease()">Decrease</b-button>
        <p>Total: {{total}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isDisplayPTag: true,
      listItems: [],
      listObjects: [
        { num1: 1, num2: 2 },
        { num1: 56, num2: 546 },
        { num1: 12, num2: 3 },
        { num1: 123, num2: 6 }
      ],
      inputNumber: 0,
      total: 0
    };
  },
  methods: {
    onSwitch() {
      this.isDisplayPTag = !this.isDisplayPTag;
    },
    onAddingItem() {
      this.listItems.push("added");
    },
    setColor(index) {
      return index % 2 !== 0 ? "odd" : "even";
    },
    isOddorEven(value) {
      return value % 2 !== 0 ? "số lẻ" : "số chẵn";
    },
    Increase() {
      return (this.total = this.total + parseInt(this.inputNumber));
    },
    Decrease() {
      return (this.total = this.total - parseInt(this.inputNumber));
    }
  }
};
</script>

<style scoped>
.mt-20 {
  margin-top: 20px;
}
.mb-20 {
  margin-bottom: 20px;
}
.odd {
  background-color: red;
  display: block;
}
.even {
  background-color: yellow;
  display: block;
}
.exercise {
  border: solid 2px black;
  margin: 20px 0px;
}
</style>
