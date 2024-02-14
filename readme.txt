v-html ใช้แสดง [data ที่มี tag html อยู่ด้วย] ในส่วน attribute ของ html 
v-bind (:) ใช้กับ data ในส่วน attribute ของ html
v-on (@) ใช้กับ function ในส่วน attribute ของ html
v-if,v-else ใช้ check condition
v-for ใช้ loop array,object
v-show เหมือน v-if แต่ต่างตรงที่ v-show ค่าจะอยู่ใน dom แล้ว แต่ v-if ต้องมาแทรก element ลง dom ในภายหลัง

data ใช้เก็บข้อมูลที่มีการเปลี่ยนแปลง
method (getter, setter) method เมื่อ re-render จะถูกเรียกใช้ใหม่
computed (getter/การคำนวณต่างๆ) เหมือน method แต่จะมีการเก็บ catch และมีการ return ค่า จะไม่ถูกเรียกใช้ใหม่เมื่อ re-render แต่จะถูกเรียกเมื่อค่ามีการเปลี่ยนแปลง
watcher ติดตามการเปลี่ยนแปลงที่เกิดขึ้นกับข้อมูล

0. install extension

    -vetur
    -autorename tag
    -color highlight
    -prettier code formatter
    -live server

1. install extension in chrome

    -vue.js devtools

2. install vue cli(command line interface)

    npm install -g @vue/cli

    -สร้าง vue application ด้วยคำสั่งเดียว
    -ติดตั้ง plugin เสริมเข้าไปใน project ได้ง่ายกว่า command
    -ทดสอบรัน application โดยจำลองของ server (localhost)

    การติดตั้ง vue cli (command line interface) จะมาพร้อมเครื่องมือ
        -babel เป็น javascript compiler ที่ทำให้สามารถเขียน java script version ใหม่ๆใน vue ได้
        -ESLint ตรวจสอบไวยากรณ์ javascript ว่าเขียนถูกต้องหรือไม่
        -webpack สำหรับจัดการและแปลงไฟล์ประเภทต่างๆ ให้อยู่ในรูปแบบที่ browser อ่านได้ เช่น ไฟล์รูปภาพ

3. โครงสร้าง project

    -src/assets folder สำหรับจัดการเกี่ยวกับ ภาพ
    -src/components เก็บ component ใน application
    -src/app.vue (root component)
    -src/main.js เป็นไฟล์ script ที่ถูกเรียกบนไฟล์ index.html โดยจะแสดงผล component ที่ id app (#app)
    -index.html เรียกไฟล์ script(main.js) เพื่อแสดง component

4. พื้นฐาน component
    
    -tag <template></template>สำหรับแสดงผล
    -tag <script></script>สำหรับเขียน javascript เพื่อควบคุมการทำงานของ component เช่น กำหนด data, method
        -function data()
    -tag <style></style> เขียน css พเื่อออกแบบและตกแต่ง template

    -App.vue
        //export component name App, กำหนด data function
        <script>
            export default {
                name: 'App',
                data(){
                    return{
                        firstName: 'woramet',
                        lastName: 'tompudsa',
                        phoneNumber: '0812345678'
                    }
                }
            }
        </script>

        <template>
            <h1 id="intro">hello woramet</h1>
            <p>{{firstName}}</p>
            <p>{{800+200}}</p>
        </template>

        <style>
            #intro{
                color: red;
            }
        </style>

5. interpolation(ใช้กับ tag template ในส่วน element) การแสดงผลข้อมูลในพื้นที่ template
    //แสดงผล ข้อมูลใน data() บน template ได้ โดยใช้ {{}}

    -App.vue

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
                    myArr: ['apple', 'banana'],
                    myObject: {gender: 'boy', status: 'single'}
                }
            }
            }
        </script>

        <template>
            <h1 id="intro">hello woramet</h1>
            <p>myname is {{getFullName()}}</p>
            <p>{{firstName}}</p>
            <p>{{800+200}}</p>
            <p>{{myArr[0]}}</p>
            <p>{{myObject.gender}}</p>
        </template>

6. v-html (ใช้กับ tag template ในส่วน attribute ของ tag htmlต่างๆ) การแสดงข้อมูลที่มี tag html ใน data()

    -App.vue

        <script>
        export default {
            name: 'App',
            data(){
                return{
                    country: '<strong>thailand<strong>'
                }
            }
        }
        </script>

        <template>
            <p>country: <span v-html="country"></span></p>
        </template>

7. method
    //การเข้าถึง properties ใน template จะใช้ interpolation {}
    //การเข้าถึง properties ใน script จะใช้ keyword: this

    -App.vue

        <script>
            export default {
            name: 'App',
            data(){
                return{
                    firstName: 'woramet',
                    lastName: 'tompudsa',
                    phoneNumber: '0812345678',
                    country: '<strong>thailand<strong>'
                }
            },
            methods:{
                getFullName(){
                    return this.firstName + this.lastName
                }
            }
            }
        </script>

        <template>
            <p>myname is {{getFullName()}}</p>
        </template>

8. v-bind ผูกค่า data กับ attribute ของ tag html 
    // (ใช้กับ tag template ในส่วน attribute ของ tag htmlต่างๆ) หรือเรียกว่า Attribute Binding
    // <img v-bind:src="imgAddr" width="100" height="200" />
    // เขียนย่อๆ <img :src="imgAddr" width="100" height="200" />

    -App.vue

        <script>
        export default {
            name: 'App',
            data(){
                imgAddr: 'https://mario.nintendo.com/static/d783068682f98d6cfec666c747a27793/d6e64/mario.png'
            },
        }
        </script>

        <template>
            <img v-bind:src="imgAddr" width="100" height="200" />
        </template>

9. v-on ผูกค่า function กับ attribute ของ tag html
    
    -event ต่างๆ (v-on: / @) เช่นการ click button ให้ใช้ v-on:click หรือ @click แทน onClick

        -App.vue

            <script>
                export default {
                name: 'App',
                data(){
                    return{
                    firstName: 'woramet',
                    }
                },
                methods:{
                    showData(){
                        alert(this.firstName)
                    }
                }
                }
            </script>

            <template>
                <button @click="showData">show</button>
            </template>

    -event argument การส่งค่า argument ไปกับ event ทำการส่งค่า 10 ไปกับ event
    
        -App.vue

            <template>
                <h2>mynumber is <strong> {{myNumber}}</strong></h2>
                <button @click="increment">increment</button>
                <button @click="incrementArg(10)">incrementArg(10)</button>
            </template>

            <script>
                export default {
                name: 'App',
                data(){
                    return{
                        myNumber: 0,
                    }
                },
                methods:{
                    increment(){
                        this.myNumber = this.myNumber + 1
                    },
                    incrementArg(value){
                        this.myNumber = this.myNumber + value
                    }
                }
                }
            </script>

    -event input

        -App.vue

            <template>
                <p>what is your nick name ? </p> <input type="text" v-on:input="setNickName">
                <p>my nickname is {{myNickName}}</p>
            </template>

            <script>
                export default {
                name: 'App',
                data(){
                    return{
                        myNickName: ''
                    }
                },
                methods:{
                    setNickName(event){
                        this.myNickName = event.target.value
                    }
                }
                }
            </script>
    
    -event modifier

        -App.vue

            <template>
                <p>my nickname is {{myNickName}}</p>
                <br>
                <button @click.left="showData">left click</button>
                <button @click.right="showData">right click</button>
                <button @click.middle="showData">middle click</button>
                <button @click.ctrl="showData">ctrl + click</button>
                <br>
                <form @submit.prevent="submitForm">
                    <label for="">ป้อนชื่อเล่น</label>
                    <input type="text" @input="setNickName">
                    <button type="submit">save</button>
                </form>
            </template>

            <script>
                export default {
                name: 'App',
                data(){
                    return{
                        myNickName: ''
                    }
                },
                methods:{
                    setNickName(event){
                        this.myNickName = event.target.value
                    },
                    submitForm(event){
                        alert("save nickname")
                        console.log(event);
                    }
                }
                }
            </script>

10. การเข้าถึง dom element (ref Dom Element)
    // จากตัวอย่างทำการอ้างอิง input ด้วย ref = inputRef
    // จากนั้นเมื่อกด submit ให้ทำการแก้ไขช่องกรอก input ที่อ้างอิงให้มีค่าว่าง

    -App.vue

        <script>
            export default {
            name: 'App',
            data(){
                return{
                    myColor: ''
                }
            },
            methods:{
                submitColor(){
                    this.myColor = this.$refs.inputRef.value
                    this.$refs.inputRef.value = ''
                }
            }
            }
        </script>

        <template>
            <form @submit.prevent="submitColor">
                <input type="text" ref="inputRef">
                <button type="submit">submitColor with ref</button>
            </form>
        </template>

11. render condition (v-if, v-else)

    -App.vue

        <template>

            <!-- if/else condition -->
            <p v-if="myHobby.length !== 0"> myHobby is {{myHobby}}</p>
            <div v-else><p>No Hobby</p></div>
            <button @click="addHobby">Add Hobby</button>
            <button @click="deleteHobby">Delete Hobby</button>
        
        </template>

        <script>
            export default {
            name: 'App',
            data(){
                return{
                    myHobby: ''
                }
            },
            methods:{
                addHobby(){
                    this.myHobby = "i like football"
                },
                deleteHobby(){
                    this.myHobby = ""
                }
            }
            }
        </script>

12. v-for ใช้ loop

    -App.vue

        <template>
            <!-- v-for Array -->
            <ul>
                <li v-for="(item, index) in myArr" :key="index">
                    {{item}}
                </li>
            </ul>

            <!-- v-for Object -->
            <ul>
                <li v-for="(item, key) in myObject" :key="key">
                    {{key}} - {{item}}
                </li>
            </ul>
        </template>

    
        <script>
        export default {
        name: 'App',
        data(){
            return{
                myArr: ['apple', 'banana', 'mango'],
                myObject: {gender: 'boy', status: 'single'},
            }
        }
        }
        </script>

13. v-show เหมือน v-if แต่ต่างตรงที่ v-show ค่าจะอยู่ใน dom แล้ว แต่ v-if ต้องมาแทรก element ลง dom ในภายหลัง

    -App.vue

        <script>
            export default {
            name: 'App',
            data(){
                return{
                    isVisible: false
                }
            },
            methods:{
                toggleVisible(){
                    this.isVisible = !this.isVisible
                }
            }
            }
        </script>

        <template>
            {{isVisible?"show":"hide"}}
            <article v-show="isVisible">
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quam aut id porro impedit sit. Fuga cupiditate nihil dolor veritatis molestias optio vitae. At tenetur, reiciendis recusandae repellendus assumenda veniam ad.
                Aliquid ullam asperiores, inventore rerum numquam ipsam exercitationem quam laboriosam pariatur reiciendis facere hic tempora nulla aspernatur culpa excepturi corporis non maxime explicabo vero omnis tempore perferendis architecto amet? Mollitia?
                Similique assumenda, magnam temporibus quam illum et, ea eveniet veritatis repudiandae earum, quisquam dolorum accusantium rem magni suscipit a? Aspernatur cupiditate sunt dicta nulla aut iusto! Quae sequi temporibus animi?
                Commodi est sunt iure? Consequuntur excepturi rem, doloribus dolorum quibusdam tempora neque sit provident reiciendis repellat sunt hic voluptatem dolor nisi, perferendis harum quis adipisci dolorem delectus veniam eius. Dolorem!
                Voluptate optio esse nemo modi sit incidunt aspernatur. A ullam reprehenderit unde ad perferendis omnis inventore cupiditate atque amet ducimus aut, praesentium sequi perspiciatis vel, laborum corporis deserunt sapiente veritatis?</p>
            </article>
            <button @click="toggleVisible">toggle lorem</button>

        </template>

14. Computed properties[method ที่มีการ return ค่า](กรองข้อมูล/คำนวณ/กำหนดเงื่อนไข/ดึงข้อมูล getter method) จะเหมือน method แต่

    //หากทำการนำ function ใน computed ไปใส่ใน method ก็สามารถทำได้ แต่เมื่อเกิดการ re-render จะทำการเรียกค่าใหม่อีกครั้ง

    //computed จะทำการ caching ค่าเอาไว้เพื่อดักการทำงานเมื่อค่าที่เราสนใจมีการเปลี่ยนแปลง
    //method จะถูกเรียกใช้ทุกครั้งที่ component re-render ใหม่ ส่วน computed จะถูกเรียกใช้เมื่อข้อมูลเปลี่ยนแปลงค่า

    //จะเห็นได้ว่าใน ส่วน getRandombyMethod() และ getRandombyComputed() มีการคำนวณค่าด้วย this.myNumber
    //หากลองกดปุ่มเพิ่มค่า จะเห็นว่า ทั้ง getRandombyMethod() และ getRandombyComputed() จะทำการคำนวณใหม่
    //หากลองกดปุ่ม addHobby หรือ deleteHobby เพื่อทำการแกไขค่า myHobby ซึ่งไม่เกี่ยวกับ myNumber ทำให้การ re-render แล้วทำให้ ค่าที่ getRandombyMethod() เปลี่ยนแต่ getRandombyComputed() ไม่เปลี่ยน

    -App.vue

        <script>
            export default {
            name: 'App',
            data(){
                return{
                    myNumber: 0,
                    myHobby: '',
                }
            },
            methods:{
                increment(){
                    this.myNumber = this.myNumber + 1
                },
                addHobby(){
                    this.myHobby = "i like football"
                },
                deleteHobby(){
                    this.myHobby = ""
                },
                getRandombyMethod(){
                    return Math.random() + this.myNumber
                }
            },
            computed:{
                getRandombyComputed(){
                    return Math.random() + this.myNumber
                }
            }
        }
        </script>

        <template>

            <button @click="addHobby">Add Hobby</button>
            <button @click="deleteHobby">Delete Hobby</button>

            <h2>mynumber is <strong> {{myNumber}}</strong></h2>
            <button @click="increment">increment</button>

            <!-- Computed -->
            {{getRandombyMethod()}}
            {{getRandombyComputed}}
        </template>

15. Watchers ทำงานกับคำสั่งที่อยู่ในรูปแบบ asynchronous ได้
    //watchers ติดตามการเปลี่ยนแปลงที่เกิดขึ้นกับข้อมูล
    //computed properties เก็บผลลัพธ์การเปลี่ยนแปลงที่เกิดขึ้น

    -App.vue

        <script>
            export default {
            name: 'App',
            data(){
                return{
                    myNumber: 0,
                }
            },
            methods:{
                increment(){
                    this.myNumber = this.myNumber + 1
                },
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

            <h2>mynumber is <strong> {{myNumber}}</strong></h2>
            <br>
            <button @click="increment">increment</button>

        </template>







