<template>
  <div>
    <nav
      class="navbar is-transparent"
      style="background-color: #6a7150; color: white"
    >
      <div class="navbar-brand">
        <div>
          <img
            class="logo"
            src="../klinnangsue_logo.svg"
            width="200"
            height="100"
          />
          <div class="logo-text">
            <span>Klinnangsue<br />ร้านกลิ่นหนังสือ</span>
          </div>
        </div>
      </div>
      <div class="navbar-start">
        <div class="navbar-item" style="margin-left: 40px">
          <a
            class="navbar-item g-navitem"
            style="margin-right: 50px; margin-left: 10px"
          @click="toHomePage()">
            Book
          </a>
          <div class="navbar-item">
            <a class="navbar-item g-navitem"> Blind date with a book </a>
          </div>
        </div>
      </div>
      <div class="navbar-end" style="margin-right: 100px">
        <div class="navbar-item">
          <div class="field is-grouped">
            <p class="control">
              <a
                class="button is-primary"
                style="font-size: 1.5rem"
              >
                <span class="icon">
                  <i class="fa-solid fa-user"></i>
                </span>
                <span
                  >Hello, <b>{{ user.username }}</b></span
                >
              </a>
            </p>
          </div>
        </div>
      </div>
    </nav>

    <div class="container">
      <div class="columns">
        <div class="column is-4">
          <div class="box ubox">
            <a class="linkinP" @click="toOrderPage()"><span> ดูคำสั่งซื้อ </span></a>
            <hr />
            <a class="linkinP" href=""><span> เพิ่มข้อมูลหนังสือ</span></a>
            <hr />
            <a class="linkinP" href="#"><span style="color: black"> เพิ่มข้อมูลผู้แต่ง </span></a>
            <hr />
            <a class="linkinP" @click="toAddPublisher()"
              ><span> เพิ่มข้อมูลสำนักพิมพ์ </span></a
            >
            <hr />
            <a class="linkinP" @click="toLogin()"
                ><span> ออกจากระบบ </span></a
              >
          </div>
        </div>
        <div class="column is-4">
          <div class="ubox" style="width: 800px">
            <div class="">
              <div class="k-box box">
                <div class="k-title title">เพิ่มข้อมูลผู้แต่ง</div>
                <div class="k-fe field">
                  <label class="label">ชื่อ</label>
                  <p class="control has-icons-left has-icons-right">
                    <input class="input" type="name" placeholder="ชื่อ" :class="{ 'is-danger': error.name }" v-model="name" @input="validName()">
                    <span class="has-text-danger">{{ error.name }}</span>
                  </p>
                </div>
                <div class="k-fe field">
                  <label class="label">นามสกุล</label>
                  <p class="control has-icons-left has-icons-right">
                    <input class="input" type="surname" placeholder="นามสกุล" :class="{ 'is-danger': error.surname }" v-model="surname" @input="validSurname()">
                    <span class="has-text-danger">{{ error.surname }}</span>
                  </p>
                </div>
                <div class="k-fe field">
                  <label class="label">นามแฝง</label>
                  <p class="control has-icons-left">
                    <input class="input" type="alias" placeholder="นามแฝง" :class="{ 'is-danger': error.alias }" v-model="alias" @input="validAlias()">
                    <span class="has-text-danger">{{ error.alias }}</span>
                  </p>
                </div>
                <div class="k-fe field">
                  <p class="control">
                    <button class="k-bu button" @click="addAuthor()">บันทึกข้อมูล</button>
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- footer -->
    <footer>
      <nav class="level k-level">
        <div class="level-item has-text-centered">
          <div>
            <p style="letter-spacing: 5" class="title has-text-white">
              Klinnangsue
            </p>
            <p style="letter-spacing: 5" class="title has-text-white">
              ร้านกลิ่นหนังสือ
            </p>
          </div>
        </div>
        <p class="level-item has-text-centered">
          <a class="link is-info has-text-white" @click="toHomePage()">ร้านหนังสือ</a>
        </p>
        <p class="level-item has-text-centered">
          <a class="link is-info has-text-white">แจ้งการโอนเงิน</a>
        </p>
        <p class="level-item has-text-centered">
          <a class="link is-info has-text-white">รู้จักเรา</a>
        </p>
        <p class="level-item has-text-centered">
          <a class="link is-info has-text-white">ติดต่อเรา</a>
        </p>
      </nav>

      <!-- Right side -->
      <div class="level-right" style="padding-right: 100px">
        <p class="level-item">
          <strong class="has-text-white">ติดตามข่าว ร้านกลิ่นหนังสือ</strong>
        </p>
      </div>
      <div class="level-right" style="padding-right: 100px">
        <div class="level-item">
          <div class="field has-addons">
            <p class="control">
              <input class="input" type="text" placeholder="EMAIL ADDRESS" />
            </p>
            <p class="control">
              <button class="button">SUBSCRIBE</button>
            </p>
          </div>
        </div>
      </div>

      <div class="level-right" style="padding-right: 100px">
        <div class="k-im-item">
          <i class="fa-brands fa-facebook"></i>
        </div>
        <div class="k-im-item">
          <i class="fa-brands fa-twitter"></i>
        </div>
        <div class="k-im-item">
          <i class="fa-brands fa-instagram"></i>
        </div>
      </div>

      <div class="level-right" style="padding-right: 100px">
        <p class="level-item">
          <a class="has-text-white">นโยบายความเป็นส่วนตัว</a>
        </p>
        <p class="level-item">
          <a class="has-text-white">นโยบายการส่งสินค้า</a>
        </p>
        <p class="level-item"><a class="has-text-white">นโยบายการคืนเงิน</a></p>
      </div>

      <p class="level-left" style="padding-left: 50px; padding-bottom: 20px">
        <a class="link is-info has-text-white"
          >Copyright©2020 Klinnangusue, All Rights Reserved.</a
        >
      </p>
    </footer>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "addAuthor",
  data() {
    return {
      user: [], // add blogs variable
      name: '',
      surname: '',
      alias: '',
      error: {
        name: '',
        surname: '',
        alias: '',
      },
    };
  },
  mounted() {
    const userId = this.$route.params.userId;
    axios.get(`http://localhost:3000/users/${userId}`).then((response) => {
      console.log(response.data);
      this.user = response.data[0];
    });
  },
  methods: {
    validName() {
      if (this.name === "") {
        this.error.name = "กรุณากรอกชื่อผู้แต่ง";
        return;
      }
      this.error.name = "";
    },
    validSurname() {
      if (this.surname === "") {
        this.error.surname = "กรุณากรอกนามสกุลผู้แต่ง";
        return;
      }
      this.error.surname = "";
    },
    validAlias() {
      if (this.alias === "") {
        this.error.alias = "กรุณากรอกนามแฝง";
        return;
      }
      this.error.alias = "";
    },
    addAuthor () {
        if (this.name == "" || this.surname == "" || this.alias == ""){
            alert("กรุณากรอกข้อมูลให้ครบ")
        }else{
        const data = {
            firstname: this.name,
            lastname: this.surname,
            alias: this.alias
        }
        console.log(data)
        axios.post(`http://localhost:3000/addAuthor`, data).then((res) => {
            console.log(res)
            if (res.data == 'update succesful!'){
                alert('เพิ่มข้อมูลสำเร็จ')
            }else if(res.data == 'error'){
                alert('มีข้อมูลผู้แต่งอยู่แล้ว')
            }
        }).catch((err) => {
            console.log(err)
        })
        this.name = '',
        this.surname = '',
        this.alias = ''
        }
    },
    toHomePage() {
        const userId = this.user.user_id
      this.$router.push(`/homePage/${userId}`)
    },
    toAddPublisher (){
      const userId = this.user.user_id
      this.$router.push(`/addPublisher/${userId}`)
    },
    toOrderPage() {
      const userId = this.user.user_id
      this.$router.push(`/orderTable/${userId}`)
    },
    toLogin() {
      this.$router.push(`/loginPage`);
    }
  },
};
</script>

<style>
.g-navitem {
  font-size: 2rem;
  color: white;
}
body {
  background: #f2e0c3;
}
.k-sec {
  background-color: #6a7150;
  margin-top: 100%;
}
.k-butt {
  background-color: #6a7150;
  color: white;
  position: relative;
}
.k-butt2 {
  background-color: #6a7150;
  color: white;
  font-size: 1.2rem;
}
.k-im-item {
  margin-top: 20px;
  margin-right: 5px;
  margin-bottom: 20px;
  font-size: 30;
}
.k-im {
  margin-right: 15px;
}
.k-box {
  width: 600px;
  margin: auto;
  margin-top: 50px;
}
.k-check {
  margin-bottom: 10px;
}
.k-pass {
  color: #6a7150;
}
.k-mem {
  color: #6a7150;
}
.k-title {
  color: #6a7150;
}
.k-bu {
  background-color: #6a7150;
  color: white;
}
.k-small {
  color: #6a7150;
  margin-bottom: 10px;
}
.ti2 {
  margin-top: 100px;
}
.clicktoblind {
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  height: 400px;
  background-image: url("../founder.jpg");
  background-size: cover;
}
.boxtoblind {
  padding: 15px;
  position: absolute;
  z-index: 1;
  width: 400px;
  background-color: #6d7352;
  color: white;
  right: 50px;
  top: 100px;
  letter-spacing: 5px;
  font-weight: bold;
  font-size: 2rem;
}
.gbuttom {
  margin-top: 30px;
  color: white;
  background-color: #6d7352;
  width: 100%;
}
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  width: 20%;
}
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
.container {
  padding: 2px 16px;
}
.booktype {
  padding: 30px;
  font-size: 2rem;
  margin-left: 60px;
}
.index {
  display: block;
  border: none;
  background-color: transparent;
  font-size: 1.2rem;
}
.logo {
  width: 150px;
  padding-left: 60px;
  padding-top: 20px;
  margin-right: 30px;
}
.logo-text {
  position: relative;
  padding-left: 40px;
  text-align: center;
  letter-spacing: 3;
}
.k-level {
  padding-top: 50px;
  margin-top: 50px;
  padding-right: 100px;
}
.k-im-item {
  font-size: 2rem;
}
.logo-text2 {
  letter-spacing: 15;
  margin-top: 40px;
  margin-left: 100px;
  font-size: 2.5rem;
  color: #6d7352;
}
.logo2 {
  width: 150px;
  padding-left: 60px;
  padding-top: 20px;
  margin-right: 30px;
  margin-left: 100px;
}
.linkinP {
  color: #6d7352;
}
.linkinP:hover {
  color: black;
}
.ubox {
  width: 300px;
  margin-top: 50px;
}
.gbookstore {
  width: 300px;
  height: 50px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 50px;
  background-color: #bf9772;
  text-align: center;
  border: none;
  border-radius: 30px;
}
.glogo {
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
  width: 200px;
}
.glogo-text {
  letter-spacing: 15;
  font-size: 2.5rem;
  color: white;
}
.gbox {
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  background-color: #6d7352;
  text-align: center;
  padding-top: 10px;
  padding-bottom: 10px;
}
.gbookstore2 {
  width: 250px;
  height: 80px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
  background-color: #bf9772;
  text-align: center;
  border: none;
  border-radius: 30px;
}
.gbutton {
  margin-top: 30px;
  text-align: center;
  background-color: none;
}
.gbutt {
  border: 2px solid #6d7352;
  font-size: 1.2rem;
  background-color: #f2e0c3;
  color: #6d7352;
  border-radius: 20px;
  width: 300px;
  height: 50px;
}
</style>