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
          <a @click="toHomePage()"
            class="navbar-item g-navitem"
            style="margin-right: 50px; margin-left: 10px"
          >
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
                @click="toOrderTable()"
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
            <a class="linkinP" @click="toOrderTable()"><span> ดูคำสั่งซื้อ </span></a>
            <hr />
            <a class="linkinP" href="#"
              ><span style="color: black"> เพิ่มข้อมูลหนังสือ</span></a
            >
            <hr />
            <a class="linkinP" @click="toAddAuthor()"><span> เพิ่มข้อมูลผู้แต่ง </span></a>
            <hr />
            <a class="linkinP" @click="toAddPublisher()"><span> เพิ่มข้อมูลสำนักพิมพ์ </span></a>
            <hr />
            <a class="linkinP" @click="toLogin()"
                ><span> ออกจากระบบ </span></a
              >
          </div>
        </div>
        <div class="column is-4">
          <div class="ubox box" style="width: 800px">
            <div class="">
            <div class="k-title title">เพิ่มข้อมูลหนังสือ</div>
            <div class="k-fe field">
                <label class="label">ชื่อหนังสือ</label>
                <p class="control has-icons-left">
                    <input class="input" type="bookname" placeholder="ชื่อหนังสือ" :class="{ 'is-danger': error.bookname }" v-model="bookname" @input="validBookName()">
                    <span class="has-text-danger">{{ error.bookname }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">ชื่อผู้แต่ง</label>
                <p class="control has-icons-left">
                    <input class="input" type="authorname" placeholder="ชื่อผู้แต่ง" :class="{ 'is-danger': error.authorname }" v-model="authorname" @input="validAuthorName()">
                    <span class="has-text-danger">{{ error.authorname }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">รูปปกหน้า</label>
                <p class="control has-icons-left">
                    <input class="input" type="frontpic" placeholder="รูปปกหน้า" :class="{ 'is-danger': error.frontpic }" v-model="frontpic" @input="validFrontpic()">
                    <span class="has-text-danger">{{ error.frontpic }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">รูปปกหลัง</label>
                <p class="control has-icons-left">
                    <input class="input" type="backpic" placeholder="รูปปกหลัง" v-model="backpic">
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">ประเภทหนังสือ</label>
                <p class="control has-icons-left has-icons-right">
                    <input class="input" type="typebook" placeholder="ประเภทหนังสือ" :class="{ 'is-danger': error.typebook }" v-model="typebook" @input="validTypebook()">
                    <span class="has-text-danger">{{ error.typebook }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">จำนวนสินค้า</label>
                <p class="control has-icons-left">
                    <input class="input" type="unit" placeholder="จำนวนสินค้า" :class="{ 'is-danger': error.unit }" v-model="unit" @input="validUnit()">
                    <span class="has-text-danger">{{ error.unit }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">ราคาสินค้า</label>
                <p class="control has-icons-left">
                    <input class="input" type="price" placeholder="ราคาสินค้า" :class="{ 'is-danger': error.price }" v-model="price" @input="validPrice()">
                    <span class="has-text-danger">{{ error.price }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">สำนักพิมพ์</label>
                <p class="control has-icons-left">
                    <input class="input" type="publisher" placeholder="สำนักพิมพ์" :class="{ 'is-danger': error.publisher }" v-model="publisher" @input="validPublisher()">
                    <span class="has-text-danger">{{ error.publisher }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">บาร์โค้ด</label>
                <p class="control has-icons-left">
                    <input class="input" type="barcode" placeholder="บาร์โค้ด" :class="{ 'is-danger': error.barcode }" v-model="barcode" @input="validBarcoder()">
                    <span class="has-text-danger">{{ error.barcode }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">ISBN</label>
                <p class="control has-icons-left">
                    <input class="input" type="isbn" placeholder="ISBN" :class="{ 'is-danger': error.isbn }" v-model="isbn" @input="validIsbn()">
                    <span class="has-text-danger">{{ error.isbn }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <label class="label">เนื้อเรื่องย่อ</label>
                <p class="control has-icons-left">
                    <textarea class="textarea" type="text" placeholder="เนื้อเรื่องย่อ" :class="{ 'is-danger': error.text }" v-model="text" @input="validText()"></textarea>
                    <span class="has-text-danger">{{ error.text }}</span>
                </p>
            </div>
            <div class="k-fe field">
                <p class="control">
                    <button class="k-bu button" @click="submitFile()">
                        บันทึกการเปลี่ยนแปลง
                    </button>
                </p>
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
  name: "addDetailBook1",
  data() {
    return {
      user: [], // add blogs variable
      bookname: '',
      authorname: '',
      frontpic: '',
      backpic: '',
      typebook: '',
      unit: '',
      price: '',
      publisher: '',
      barcode: '',
      isbn: '',
      text: '',
      error: {
        bookname: '',
        authorname: '',
        frontpic: '',
        backpic: '',
        typebook: '',
        unit: '',
        price: '',
        publisher: '',
        barcode: '',
        isbn: '',
        text: ''
      }
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
    validCodeBook() {
      if (this.codebook === "") {
        this.error.codebook = "กรุณากรอกรหัสหนังสือ";
        return;
      }
      if (this.codebook.length > 10 ) {
        this.error.codebook = "รหัสหนังสือต้องน้อยกว่า 10 หลัก";
        return;
      }
      this.error.codebook = "";
    },
    validBookName() {
      if (this.bookname === "") {
        this.error.bookname = "กรุณากรอกชื่อหนังสือ";
        return;
      }
      this.error.bookname = "";
    },
    validAuthorName() {
      if (this.authorname === "") {
        this.error.authorname = "กรุณากรอกชื่อผู้แต่ง";
        return;
      }
      this.error.authorname = "";
    },
    validTranslatename() {
      if (this.translatename === "") {
        this.error.translatename = "กรุณากรอกชื่อผู้แปล";
        return;
      }
      this.error.translatename = "";
    },
    validDrawname() {
      if (this.drawname === "") {
        this.error.drawname = "กรุณากรอกชื่อผู้วาด";
        return;
      }
      this.error.drawname = "";
    },
    validFrontpic(){
      if (this.frontpic === "") {
        this.error.frontpic = "กรุณาใส่รูปปกหน้า";
        return;
      }
      this.error.frontpic = "";
    },
    validTypebook() {
      if (this.typebook === "") {
        this.error.typebook = "กรุณาใส่ประเภทหนังสือ";
        return;
      }
      this.error.typebook = "";
    },
    validUnit() {
      if (this.unit === "") {
        this.error.unit = "กรุณาใส่จำนวนหนังสือ";
        return;
      }
      if (isNaN(this.unit)) {
        this.error.unit = "จำนวนหนังสือต้องเป็นตัวเลข";
        return;
      }
      this.error.unit = "";
    },
    validPrice() {
      if (this.price === "") {
        this.error.price = "กรุณาใส่ราคาหนังสือ";
        return;
      }
      if (isNaN(this.price)) {
        this.error.price = "ราคาหนังสือต้องเป็นตัวเลข";
        return;
      }
      this.error.price = "";
    },
    validPublisher() {
      if (this.publisher === "") {
        this.error.publisher = "กรุณาใส่ชื่อสำนักพิมพ์";
        return;
      }
      this.error.publisher = "";
    },
    validBarcoder() {
      if (this.barcode === "") {
        this.error.barcode = "กรุณาบาร์โค้ด";
        return;
      }
      this.error.barcode = "";
    },
    validIsbn() {
      if (this.isbn === "") {
        this.error.isbn = "กรุณากรอกเลข ISBN";
        return;
      }
      if (this.isbn.length != 13) {
        this.error.isbn = "กรุณากรอกเลข ISBN 13 หลัก";
        return;
      }
      if (isNaN(this.isbn)) {
        this.error.isbn = "ต้องเป็นตัวเลขทั้งหมด";
        return;
      }
      this.error.isbn = "";
    },
    validText() {
      if (this.text === "") {
        this.error.text = "กรุณาใส่เนื้อเรื่องย่อ";
        return;
      }
      this.error.text = "";
    },
    submitFile() {
      if (this.bookname == '' ||
        this.authorname == '' ||
        this.typebook == '' ||
        this.unit == '' ||
        this.price == '' ||
        this.publisher == '' ||
        this.barcode == '' ||
        this.isbn == '' ||
        this.text == '' ||
        this.frontpic == '' ||
        this.backpic == ''){
          alert('กรุณากรอกข้อมูลให้ครบ')
        }else{
          const data = {
            bookname: this.bookname,
            authorname: this.authorname,
            typebook: this.typebook,
            unit: this.unit,
            price: this.price,
            publisher: this.publisher,
            barcode: this.barcode,
            isbn: this.isbn,
            text: this.text,
            frontpic: this.frontpic,
            backpic: this.backpic
        }
      axios
        .post(`http://localhost:3000/book/addBook`, data)
        .then((response) => {
          alert(response.data)
        });
        this.bookname = '',
        this.authorname = '',
        this.typebook = '',
        this.unit = '',
        this.price = '',
        this.publisher = '',
        this.barcode = '',
        this.isbn = '',
        this.text = '',
        this.frontpic = '',
        this.backpic = ''
        }
        
    },
    toAddPublisher (){
      const userId = this.user.user_id
      this.$router.push(`/addPublisher/${userId}`)
    },toAddAuthor() {
        const userId = this.user.user_id
      this.$router.push(`/addAuthor/${userId}`)
    },
    toHomePage() {
        const userId = this.user.user_id
      this.$router.push(`/homePage/${userId}`)
    },
    toLogin() {
      this.$router.push(`/loginPage`);
    },
    toOrderTable() {
      const userId = this.user.user_id
      this.$router.push(`/orderTable/${userId}`)
    }
  }
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