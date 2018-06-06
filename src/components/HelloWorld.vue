<template>
  <div class="hello">
    <div id="container">
      <div id="menuLeft">
        <input type="text" v-model="newUser.name" style="width:48%;padding:2% 0% 2% 0%;font-size:40px;">
        <input type="number" v-model="newUser.age" style="width:48%;padding:2% 0% 2% 0%;font-size:40px;">
        <button type="button" @click="add()" style="width:98%;font-size:1em;">GOGO</button>
      </div>

      <div id="menuRight">
        <div v-for="(i,index) in data" :key="index">
          <table id="boxs">
            <tr>
              <td>Name</td>
              <td>:</td>
              <td> {{i.name}} </td>
              <td><button type="button" @click="edit(i)" id="btnDel">EDIT</button></td>
            </tr>
            <tr>
              <td>Age</td>
              <td>:</td>
              <td> {{i.age}} </td>
              <td><button type="button" @click="remove(i)" id="btnDel">REMOVE</button></td>
            </tr>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyCgkfHV6tYVDtnT_3qZlBjewLSEsUesRFU',
  authDomain: 'spacesex-25a91.firebaseapp.com',
  databaseURL: 'https://spacesex-25a91.firebaseio.com',
  projectId: 'spacesex-25a91',
  storageBucket: 'spacesex-25a91.appspot.com',
  messagingSenderId: '566973074118'
}
let app = Firebase.initializeApp(config)
let db = app.database()
let dataRef = db.ref('data')
export default {
  name: 'HelloWorld',
  data () {
    return {
      newUser: {
        name: '',
        age: ''
      },
      msg: 'Welcome to Your Vue.js App'
    }
  },
  firebase: {
    data: dataRef
  },
  methods: {
    add () {
      dataRef.push(this.newUser)
      this.newUser.name = ''
      this.newUser.age = ''
    },
    remove (i) {
      dataRef.child(i['.key']).remove()
    }
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css?family=Roboto');
#container{
  height:10000px;
  background-color: red;
}
#menuLeft{
  height: 100%;
  width:50%;
  float:left;
  background-color: rgb(247, 166, 185);
}
#menuRight{
  height: 100%;
  width:50%;
  float:right;
  background-color: black;
  color:wheat;
}
#boxs{
  font-family: 'Roboto', sans-serif;
  text-align: left;
  background-color: rgb(247, 166, 185);
  padding:0% 5% 0% 5%;
  width:30%;
  margin:5%;
  font-size: 40px;
  color:black;
  box-shadow: 1px 1px 1px rgb(128, 148, 147)
}
#btnDel{
  font-family: 'Roboto', sans-serif;
  padding:0% 24% 0% 24%;
  cursor: pointer;
  margin-left: 4%;
  background-color: black;
  color: rgb(247, 166, 185);
  border: none;
  width:98%;
  font-size:1em;
  transition: all linear 0.3s;
}
#btnDel:hover{
  color: black;
  background-color: rgb(247, 166, 185);
}
</style>
