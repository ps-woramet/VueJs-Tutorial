<script>
export default {
  name: 'App',
  data(){
    return{
      firstName: 'woramet',
      lastName: 'tompudsa',
      phoneNumber: '0812345678',
      country: '<strong>thailand<strong>',
      imgAddr: 'https://mario.nintendo.com/static/d783068682f98d6cfec666c747a27793/d6e64/mario.png',
      myNumber: 0,
      myArr: ['apple', 'banana', 'mango'],
      myObject: {gender: 'boy', status: 'single'},
      myNickName: '',
      myColor: '',
      myHobby: '',
      isVisible: false,
    }
  },
  methods:{
    // return เมื่อต้องการแสดงค่าบน template ด้วย interpolation และ ค่าไม่ถููกแก้ไข
    getFullName(){
      return this.firstName + this.lastName
    },
    showData(){
      alert(this.firstName)
    },
    increment(){
      this.myNumber = this.myNumber + 1
    },
    incrementArg(value){
      this.myNumber = this.myNumber + value
    },
    setNickName(event){
      this.myNickName = event.target.value
    },
    submitForm(event){
      alert("save nickname")
      console.log(event);
    },
    submitColor(){
      this.myColor = this.$refs.inputRef.value
      this.$refs.inputRef.value = ''
    },
    addHobby(){
      this.myHobby = "i like football"
    },
    deleteHobby(){
      this.myHobby = ""
    },
    toggleVisible(){
      this.isVisible = !this.isVisible
    },
    getRandombyMethod(){
      return Math.random() + this.myNumber
    }
  },
  computed:{
    getRandombyComputed(){
      return Math.random() + this.myNumber
    }
  },
  watch:{
    myNumber(value){
      if(value > 10){
        alert('value more than 10')
      }
    }
  }
}
</script>

<template>

  <h1 id="intro">hello woramet</h1>

  <!-- interpolation -->
  <p>myname is {{getFullName()}}</p>
  <p>{{firstName}}</p>
  <p>{{800+200}}</p>
  <p>{{myArr[0]}}</p>
  <p>{{myObject.gender}}</p>

  <!-- v-html for data -->
  <p>country: <span v-html="country"></span></p>

  <!-- v-bind for function เขียนย่อโดยใช้ :src="imgAddr" -->
  <img v-bind:src="imgAddr" width="100" height="200" />
  <img :src="imgAddr" width="100" height="200" />

  <!-- v-on หรือ event เชียนย่อโดยใช้ @click="showData" -->
  <h2>mynumber is <strong> {{myNumber}}</strong></h2>
  <br>
  <button v-on:click="showData">show</button>
  <button @click="increment">increment</button>

  <!-- event arg -->
  <button @click="incrementArg(10)">incrementArg(10)</button>

  <!-- event modifier -->
  <button @click.left="showData">left click</button>
  <button @click.right="showData">right click</button>
  <button @click.middle="showData">middle click</button>
  <button @click.ctrl="showData">ctrl + click</button>
  <br>

  <p>what is your nick name ? </p> <input type="text" v-on:input="setNickName">
  <p>my nickname is {{myNickName}}</p>
  <br>
  <form @submit.prevent="submitForm">
    <label for="">ป้อนชื่อเล่น</label>
    <input type="text" @input="setNickName">
    <button type="submit">save</button>
  </form>
  <br>

  <!-- ref dom element -->
  <p>color is {{myColor}}</p>
  <form @submit.prevent="submitColor">
    <input type="text" ref="inputRef">
    <button type="submit">submitColor with ref</button>
  </form>

  <!-- v-if,v-else if/else condition -->
  <p v-if="myHobby.length !== 0"> myHobby is {{myHobby}}</p>
  <div v-else><p>No Hobby</p></div>
  <button @click="addHobby">Add Hobby</button>
  <button @click="deleteHobby">Delete Hobby</button>

  <!-- v-for -->

    <!-- Array -->
    <ul>
      <li v-for="(item, index) in myArr" :key="index">
          {{item}}
      </li>
    </ul>

    <!-- Object -->
    <ul>
      <li v-for="(item, key) in myObject" :key="key">
          {{key}} - {{item}}
      </li>
    </ul>

  <!-- v-show -->
  {{isVisible?"show":"hide"}}
  <article v-show="isVisible">
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quam aut id porro impedit sit. Fuga cupiditate nihil dolor veritatis molestias optio vitae. At tenetur, reiciendis recusandae repellendus assumenda veniam ad.
    Aliquid ullam asperiores, inventore rerum numquam ipsam exercitationem quam laboriosam pariatur reiciendis facere hic tempora nulla aspernatur culpa excepturi corporis non maxime explicabo vero omnis tempore perferendis architecto amet? Mollitia?
    Similique assumenda, magnam temporibus quam illum et, ea eveniet veritatis repudiandae earum, quisquam dolorum accusantium rem magni suscipit a? Aspernatur cupiditate sunt dicta nulla aut iusto! Quae sequi temporibus animi?
    Commodi est sunt iure? Consequuntur excepturi rem, doloribus dolorum quibusdam tempora neque sit provident reiciendis repellat sunt hic voluptatem dolor nisi, perferendis harum quis adipisci dolorem delectus veniam eius. Dolorem!
    Voluptate optio esse nemo modi sit incidunt aspernatur. A ullam reprehenderit unde ad perferendis omnis inventore cupiditate atque amet ducimus aut, praesentium sequi perspiciatis vel, laborum corporis deserunt sapiente veritatis?</p>
  </article>
  <button @click="toggleVisible">toggle lorem</button>
 
  <!-- Computed -->
  {{getRandombyMethod()}}
  {{getRandombyComputed}}

</template>

<style>
  #intro{
    color: red;
  }
</style>
