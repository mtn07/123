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
                @click="toDetailProfile()"
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
            <a class="linkinP" href="#" style="color: black"
              ><span> คำสั่งซื้อ </span></a
            >
            <hr />
            <a class="linkinP" @click="toAddress()"><span> ที่อยู่</span></a>
            <hr />
            <a class="linkinP" @click="toDetailProfile()"><span> รายละเอียดบัญชี </span></a>
            <hr />
            <a class="linkinP" @click="toLogin()"><span> ออกจากระบบ </span></a>
            <hr />
          </div>
        </div>
        <div class="column is-8">
          <div class="k-boxu box">
            <div class="k-title ti1 subtitle">
              <p v-if="cart_item.length == 0">ยังไม่มีการสั่งซื้อ</p>
              <a
                class="button is-info"
                style="margin-right: 80px"
              @click="toHomePage()">
                <span class="icon">
                  <i class="fa-solid fa-shop"></i>
                </span>
                <span>เลือกดูสินค้า</span>
              </a>
            </div>
            <div v-for="book in cart_item" :key="book.book_id">
              <div class="media">
                <div class="media-left">
                  <figure class="image is-96x96">
                    <img :src="book.image_url1" alt="Placeholder image" />
                  </figure>
                </div>
                <div class="media-content pt-2">
                  <p class="is-5">{{ book.title }}</p>
                  <div style="display: flex; justify-content: space-between">
                    <div>
                      <!-- ราคาสินค้า------------------------------------------------ -->
                      <span class="is-6 has-text-info"> ราคา : {{ book.price }} บาท</span>
                      <!-- จำนวนสินค้า----------------------------------------------- -->
                      <span> จำนวน {{ book.quantity }} เล่ม</span>
                    </div>
                    <div>
                      <!-- icon รูปถังขยะ------------------------------------------- -->
                      <span
                        class="icon mr-2"
                        key="false"
                        @click="removeFromCart(book)"
                      >
                        ยกเลิก
                        <i class="far fa-trash-alt"></i>
                      </span>
                    </div>
                  </div>
                </div>
              </div>
              <hr />
            </div>
            <p>
              ราคารวมทั้งหมด : <b>{{ cart.total_price }}</b> บาท
            </p>
          </div>
          <div class="gconfirm">
            <button class="button is-success" @click="toBillPage()"> <b>ยืนยันคำสั่งซื้อ</b> </button>
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
          <a class="link is-info has-text-white" @click="toBillPage()">แจ้งการโอนเงิน</a>
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
  name: "memberOrder",
  data() {
    return {
      user: [], // add blogs variable
      showadd1: false,
      showadd2: false,
      cart: [],
      cart_item: [],
      show_modal: false,
    };
  },
  mounted() {
    const userId = this.$route.params.userId;
    axios.get(`http://localhost:3000/users/${userId}`).then((response) => {
      console.log(response.data);
      this.user = response.data[0];
    });
    axios.get(`http://localhost:3000/user/cart/${userId}`).then((response) => {
        this.cart = response.data[0]
        console.log(response.data)
    })
    axios.get(`http://localhost:3000/user/cart_item/${userId}`).then((response) => {
        console.log(response.data)
        this.cart_item = response.data
    });
  },
  methods: {
    removeFromCart(book) {
        const bookId = book.book_id
        const userId = this.user.user_id
        const cartId = this.cart.cart_id
      var r = confirm("คณต้องการยืนยันที่จะยกเลิกออเดอร์หรือไม่");
      if (r == true) {
        axios.delete(`http://localhost:3000/deleteFromCart/${userId}/${bookId}/${cartId}`).then((response) => {
            alert('ลบออกจากตะกร้าแล้ว')
            this.cart_item = response.data
        }).catch((err) => {
            console.log(err)
        })
      } else {
        alert("ไม่มีการเปลี่ยนแปลง");
      }
    },
    toHomePage () {
        const userId = this.user.user_id
        this.$router.push(`/homePage/${userId}`)
    },
    toDetailProfile() {
      const userId = this.user.user_id
      this.$router.push(`/detailProfile/${userId}`)
    },
    toBillPage(){
      const userId = this.user.user_id
      this.$router.push(`/billPage/${userId}`)
    },
    toAddress () {
      const userId = this.user.user_id
      this.$router.push(`/customerAddress/${userId}`)
    },
    toLogin() {
      this.$router.push(`/loginPage`);
    }

  },
};
</script>

<style>

.gconfirm{
  position: absolute;
  right: 0;
  margin-right: 20px;
}
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

.k-boxu{
    margin-top: 50px;
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