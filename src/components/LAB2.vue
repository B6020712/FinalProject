<template>
  <div>
    <v-row>
      <v-col>
        <v-card class="mx-auto" max-width="900px" min-height="100px">
          <br />
          <div class="display-3 mb-3 text-center">LAB 2</div>
          <div class="title font-regular text-center">IP Addressing</div>
          <div align="center" justify="center">
            <v-img height="600px" src="@/assets/lab/lab2/lab2-1.png"></v-img><br/>
          </div>
          <div class="title font-regular text-center">ไฟล์แลป: <a :href='downLoadURL'>คลิกเพื่อดาว์นโหลดไฟล์แลป</a></div><br/>
        </v-card>
      </v-col>

      <v-col>
        <v-card class="mx-auto" max-width="900px" min-height="100px">
          <br/>
          <v-row align="center" justify="center">
            <v-card-text>
              <p class="headline text--primary text-center">อธิบายแลป</p>
              <p class="subtitle-1 text--primary mainP">
                บริษัท A ได้รับ Block of Address จาก ISP เริ่มที่ 172.16.0.0/16 โดยบริษัท A มีทั้งหมด 2 สาขาย่อย<br/>
                - สาขาที่ 1 มีจำนวน Host ทั้งหมด 4000 เครื่อง<br/>
                - สาขาที่ 2 มีจำนวน Host ทั้งหมด 2000 เครื่อง<br/>
                สิ่งที่ต้องทำคือจัดสรร IP Address ให้กับสาขาที่ 1 และ สาขาที่ 2 โดย<br/>
                > จัดสรร IP Address ให้กับ Interface ของ Router แต่ละสาขาเป็น IP Address แรกที่ใช้ได้<br/>
                > จากนั้นจัดสรร IP Address ให้กับ Host ของทั้งสองสาขาโดยให้ Host เครื่องใดก็ได้มี IP Address ที่เป็นเลขสุดท้ายที่ใช้ได้<br/>
                > IP Address ของบริษัท A เริ่มตั้งแต่ 172.16.0.1 เป็นต้นไป<br/>
                > จากนั้นทำให้ Host ของทั้งสองสาขาสามารถ Ping หากันได้
              </p>
              <!-- <p class="subtitle-1">
                คำสั่งที่ใช้คือ<br/>
                Router(config)# interface g0/0 หรือ Router(config)# interface g0/1<br/>
                Router(config-if)# ip address 192.168.x.x 255.255.x.x<br/>
                Router(config-if)# no shutdown<br/>
              </p> -->

              <!-- <div>
                <br /><h1 class="text--red">*** สำหรับทดสอบ Download (ไฟล์ตัวอย่างเป็นไฟล์ของแลป 3-1) ***</h1><br />
                <v-row>
                  <v-col cols="2"><h3 class="text--primary"><strong>ไฟล์การบ้าน:</strong></h3></v-col>
                  <v-col><h3 style="text-align: left"><a :href='downLoadURL'>คลิกเพื่อดาว์นโหลดไฟล์การบ้าน</a></h3></v-col>
                </v-row><br />
              </div>
              
              <v-divider></v-divider>

              <div v-if="!readyToDoQuest">
                <br />
                <h1>คำถามหลังการทดลอง</h1><br />
                <div>คำถามมีทั้งหมด 2 ข้อ เป็นแบบ choice</div>
                <div>เมื่อทำเสร็จแล้วจะสามารถส่งไฟล์ได้</div><br />
                <v-btn color="indigo" @click="requestQuest">Question</v-btn>
              </div> -->

              <div class="d-flex justify-space-around mb-6 outlined">
                <v-spacer></v-spacer>
                <v-btn @click="labresult" color="red">Result</v-btn>
                <v-spacer></v-spacer>
                <v-btn @click="labcommand" color="primary">Command</v-btn>
                <v-spacer></v-spacer>
                <v-btn @click="gotoHomework" color="green">Homework</v-btn>
                <v-spacer></v-spacer>
              </div>

              <div v-if="result">
                <v-divider></v-divider><br />
                <h1 class="headline text--primary mainP">ผลลัพธ์ของการทำแลป</h1><br/>
                <div align="center" justify="center">
                  <v-img height="600" src="@/assets/lab/lab2/lab2result1.png"></v-img><br/>
                  <p class="subtitle-1 mainP" style="margin-top: 5px">
                    ทำการ ping และ tracert จาก PC3 ไปยัง PC 0  
                  </p>
                  <v-img width="600" src="@/assets/lab/lab2/lab2result2.png"></v-img><br/>
                </div>
              </div>

              <div v-if="command">
                <v-divider></v-divider><br />
                <h1 class="headline text--primary mainP">คำสั่งที่ใช้</h1>
                <p class="subtitle-1 mainP" style="margin-top: 5px">
                  > Router(config)# interface g0/0/0 หรือ Router(config)# interface g0/0/1<br/>
                  > Router(config-if)# ip address 172.16.x.x 255.255.x.x<br/>
                  > Router(config-if)# no shutdown<br/>
                </p>
              </div>
              

              <!-- <div v-if="readyToDoQuest">
                <br />
                <h1 class="text--primary" style="text-align: center">คำถามก่อนส่ง Assignment</h1>
                <v-radio-group v-model="quest1.title">
                  <div>{{quest1.headermsg}}</div>
                  <v-radio v-for="citem in choice1" :key="citem.no" :value="citem.no" :label="citem.msg"></v-radio>
                </v-radio-group>
                <v-radio-group v-model="quest2.title">
                  <div>{{quest2.headermsg}}</div>
                  <v-radio v-for="citem in choice2" :key="citem.no" :value="citem.no" :label="citem.msg"></v-radio>
                </v-radio-group>

                <div v-if="passSign">
                  <p class="subtitle-1 text--primary" style="text-align: center"><strong>สำหรับส่งไฟล์ .pkt ไปที่ Classroom</strong></p>
                  <v-row>
                    <v-col cols="8">
                      <template><v-file-input show-size counter v-model="myFiles" accept="image/*" @change="handleUpload($event.target.files)" label="File input"></v-file-input></template>
                      <template><v-file-input v-model="myFiles" accept="image/*" @change="handleUpload($event.target.files)" label="File input"></v-file-input></template>
                      <v-progress-circular v-if="uploadingFile" :value="timevalue" :rotate="360" :width="2" color="teal">{{timevalue}}</v-progress-circular>
                      <div v-if="uploadingFile">Progress : {{uploadValue.toFixed() + "%"}} <progress :value="uploadValue" max="100"></progress></div>
                    </v-col>
                    <v-col cols="2">
                      <v-btn color="primary" @click="uploadFile">Upload<v-icon>mdi-file-upload-outline</v-icon></v-btn>
                    </v-col>
                    <v-col cols="2">
                      <v-btn color="green" @click="toLab3">LAB 3<v-icon>mdi-arrow-right-bold-box-outline</v-icon></v-btn>
                    </v-col>
                  </v-row>
                </div>

                <div class="d-flex justify-space-around mb-6 outlined">
                  <div v-if="checked" class="pa-2 outlined"><v-btn color="red" @click="checkResult(quest1.title, quest2.title)">Check</v-btn></div>
                  <login-component v-bind:storeToken="access_Token" />
                  <div class="pa-2 outlined"><v-btn color="indigo" @click="ClassroomConnect">Classroom</v-btn></div>
                </div>
              </div> -->
            </v-card-text>
          </v-row>
        </v-card>
      </v-col>
      <!-- End Here -->
    </v-row>
  </div>
</template>

<script>
// import axios from 'axios'
import firebase from 'firebase/app';
import 'firebase/auth';
import { storage } from '../main';
import LoginComponent from './LoginComponent.vue';
const gaxios = require('gaxios');

/* eslint-disable */
export default {
  components: { LoginComponent },
  data() {
    return {
      command: false,
      result: false,
      // access_Token: '',
      downLoadURL: '',
      readyToDoQuest: false,
      name: 'LAB2',
      quest1: { title: 'lab2_no1', headermsg: '1. Right Group เป็น Classful แบบใด' },
      quest2: { title: 'lab2_no2', headermsg: '2. Left Group เป็น Classful แบบใด' },
      choice1: [
        { no: 1, msg: 'A' },
        { no: 2, msg: 'B' },
        { no: 3, msg: 'C' },
        { no: 4, msg: 'D' },
      ],
      choice2: [
        { no: 1, msg: 'E' },
        { no: 2, msg: 'Z' },
        { no: 3, msg: 'G' },
        { no: 4, msg: 'DA' },
      ],
      dialog: false,
      lab2_no1: Number,
      lab2_no2: Number,
      passSign : false,
      checked: true,
      user : {
        email : '',
        refreshToken : ''
      },
      interval: {},
      myFiles: null,
      file: null,
      timevalue: 0,
      uploadValue: 0,
      uploadingFile: false,
    }
  },
  created() {
    // console.log("access token from login comp = ")
    firebase.auth().onAuthStateChanged(user => {
      var lab2_Student = storage.ref().child('lab/lab2_Student.pkt');
      lab2_Student.getDownloadURL()
      .then((url) => {
        this.downLoadURL = url;
      })
      .catch((error) => {
        switch (error.code) {
          case 'storage/object-not-found':
            break;
          case 'storage/unauthorized':
            break;
          case 'storage/canceled':
            break;
          case 'storage/unknown':
            break;
        }
      });
      
      this.logInSign = !!user;
      if(user) {
        this.email = user.email;
        this.refreshToken = user.refreshToken;
      }

      gaxios.instance.defaults = {
        baseURL: 'https://classroom.googleapis.com/v1/',
        headers: {
          'Access-Control-Allow-Origin': '*',
          Authorization: `${access_Token}`
          // Authorization: `Bearer ${access_Token}`
        }
      }
      
    })
  },
  methods: {
    gotoHomework() { this.$router.push('/lab2_hw'); },
    toLab3() { 
      this.$router.push("/lab3"); 
    },
    checkResult (LAB2_NO1, LAB2_NO2) {
      if (LAB2_NO1 == 3 && LAB2_NO2 == 1) { 
        this.passSign = true;
        this.checked = false;
        return console.log("Pass. Good Job! You can sent .pkt file"); 
      }
      else {
        this.passSign = false;
        return console.log("Not pass!");
      }
    },
    handleUpload(event) { 
      this.file = "";
      this.myFiles = event.target.files[0];
    },
    uploadFile() {
      this.timevalue = 0;
      this.uploadValue = 0;
      var metadata = { contentType: this.myFiles.type };
      const uploadTask = storage.ref().child(this.email + "/LAB2/" + this.myFiles.name).put(this.myFiles, metadata);
      uploadTask.on(firebase.storage.TaskEvent.STATE_CHANGED, (snapshot) => {
        console.log( snapshot.bytesTransferred / snapshot.totalBytes ) * 100;
        this.uploadingFile = true;
        this.uploadValue = ( snapshot.bytesTransferred / snapshot.totalBytes ) * 100;
        this.interval = setInterval(() => {
          if (this.timevalue == this.uploadValue) {
            this.timevalue = 0
          } 
          this.timevalue += 1
        })
      }, error => { console.log(error.message) },
      () => { 
        this.uploadingFile = false; 
        storage.ref().child(this.email + "/LAB2/" + this.myFiles.name).getDownloadURL().then(function(url) { console.log(url); });
      });
    },
    labresult() { 
      this.result = true; 
      if (this.command == true) {
        this.command = false;
      }
    },
    labcommand() { 
      this.command = true;
      if (this.result == true) {
        this.result = false;
      }
    },
    // gotoHomework() {
    //   this.$router.push('/lab2_hw');
    // },
    // requestQuest() { this.readyToDoQuest = true; },
    // ClassroomConnect() {
    //   var courseId = 343458567331;
    //   var courseWorkId = 343458567494;
    //   var id = 'Cg4ItcCBm7ABEMaq573_CQ'; // bosslove242@gmail.com
    //   const url = 'courses/' + courseId + '/courseWork/' + courseWorkId + '/studentSubmissions/' + id + ':turnIn';
    //   // const url = 'courses/' + courseId + '/courseWork';
    //   async function quickstart() {
    //     console.log("This is URL = " + url);
    //     // const res = await gaxios.request({url});

    //     /* เจอเออเร่อแล้ว ต้องอ่านที่ npm ของ gaxios ตรง content-head */
    //     const res = await gaxios.request({
    //       url: url,
    //       method: "POST",
    //       // headers: { 
    //       //   'Access-Control-Allow-Origin': '*',
    //       //  }
    //     })
    //     console.log(`status: ${res.status}`);
    //     console.log('data:');
    //     console.log(res.data);
    //   }
    //   quickstart().catch(error => console.log("error occured in Lab2 ClassroomConnect(), " + error));
    // }
  }
};
</script>

<style scoped>
.v-progress-circular {
  margin: 1rem;
}
.mainP {
  padding-left: 20px;
}
</style>