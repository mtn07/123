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
            @click="toHomePage()"
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
            <p class="control" v-if="user.user_type == 'customer'">
              <a
                class="button is-primary"
                style="font-size: 1.5rem"
                @click="toCartPage()"
              >
                <span class="icon">
                  <i class="fa-solid fa-cart-shopping"></i>
                </span>
              </a>
            </p>
            <p class="control">
              <a
                class="button is-primary"
                style="font-size: 1.5rem"
                @click="toDetailPage()"
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
    <br />
    <div class="container">
      <div class="clicktoblind">
        <p class="boxtoblind">
          Don't JUDGE a book by its COVER
        </p>
      </div>

      <div class="columns">
        <div class="column">
          <div class="select is-success">
            <select name="BookType" @change="onChange()" v-model="selected">
              <option value="">หนังสือทั้งหมด</option>
              <option value="หนังสือมาใหม่">หนังสือมาใหม่</option>
              <option value="Blind Date With a Book">Blind Date With a Book</option>
              <option value="Best Sellers">Best Sellers</option>
              <option value="PRE-ORDER">PRE-ORDER</option>
              <option value="วรรณกรรมไทย">วรรณกรรมไทย</option>
              <option value="วรรณกรรมแปล">วรรณกรรมแปล</option>
              <option value="นวนิยายไทย">นวนิยายไทย</option>
              <option value="นวนิยายแปล">นวนิยายแปล</option>
              <option value="บทกวี">บทกวี</option>
              <option value="เรื่องสั้น">เรื่องสั้น</option>
              <option value="ปรัชญา">ปรัชญา</option>
              <option value="แฟนตาซี">แฟนตาซี</option>
              <option value="นักเขียนอิสระ">นักเขียนอิสระ</option>
              <option value="หนังสือเด็กๆ">หนังสือเด็กๆ</option>
            </select>
          </div>
        </div>
        <div class="column">
          <div class="columns">
            <div class="column is-half">
              <input
                class="input"
                type="text"
                v-model="search"
                placeholder="Search book(s)"
              />
            </div>
            <div class="column is-half">
              <button @click="searchBook()" class="button">Search</button>
            </div>
          </div>
        </div>
      </div>

      <!-- v-for information-->

      <div class="columns is-multiline">
        <div
          class="column is-one-fifth"
          v-for="book in books"
          :key="book.book_id"
        >
          <div
            class="card"
            style="width: 250px; height: 500px; overflow: visible"
          >
            <a>
              <router-link
                :to="{ path: `/book/${book.book_id}/${user.user_id}` }"
              >
                <div class="card-image" style="overflow: hidden">
                  <figure class="image">
                    <img
                      :src="book.image_url1"
                      alt="Placeholder image"
                      style="height: 300px"
                    />
                  </figure>
                </div>
                <div class="card-content">
                  <div
                    class="content"
                    style="
                      text-align: left;
                      overflow-wrap: break-word;
                      line-height: 1.2;
                    "
                  >
                    <p>
                      <span style="font-size: 1.2rem"
                        ><b>{{ book.title }}</b></span
                      >
                    </p>
                    <p>
                      <span style="color: #6d7352"
                        >เขียนโดย {{ book.alias }}</span
                      >
                    </p>
                    <p>
                      <span style="color: red; font-size: 1.1rem"
                        ><b>{{ book.price }}฿</b></span
                      >
                    </p>
                  </div>
                </div>
              </router-link>
            </a>
            <div class="gsetedit">
              <div v-if="user.user_type == 'admin'">
                <button
                  class="geditbutt button is-success"
                  @click="toEdit(book)"
                >
                  <b>Edit</b>
                </button>
              </div>
              <div v-if="user.user_type == 'admin'">
                <button
                  class="gdeletebutt button is-danger"
                  @click="toDelete(book)"
                >
                  <b>Delete</b>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

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
          <a class="link is-info has-text-white">ร้านหนังสือ</a>
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
  name: "homePage",
  data() {
    return {
      books: [], // add blogs variable
      user: [],
      search: "",
      cart: [],
      selected: "",
    };
  },
  mounted() {
    axios.get(`http://localhost:3000/`).then((response) => {
      console.log(response.data);
      this.books = response.data;
    });
    const userId = this.$route.params.userId;
    axios.get(`http://localhost:3000/users/${userId}`).then((response) => {
      console.log(response.data);
      this.user = response.data[0];
    });
    axios.get(`http://localhost:3000/user/cart/${userId}`).then((response) => {
      if (response.data != []) {
        this.cart = response.data;
      }
    });
    axios
      .post(`http://localhost:3000/user/creatCart/${userId}`)
      .then((response) => console.log(response.data))
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    searchBook() {
      const data = { search: this.search };
      axios
        .post(`http://localhost:3000/book/search`, data)
        .then((response) => {
          console.log(response.data);
          this.books = response.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    toDetailPage() {
      const userId = this.user.user_id;
      const userType = this.user.user_type;
      if (userType == "admin") {
        this.$router.push(`/orderTable/${userId}`);
      } else if (userType == "customer") {
        this.$router.push(`/detailProfile/${userId}`);
      }
    },
    toEdit(book) {
      const bookId = book.book_id;
      const userId = this.user.user_id;
      this.$router.push(`/editDetailBook/${userId}/${bookId}`);
    },
    toDelete(book) {
      const bookId = book.book_id;
      const result = confirm(`Are you sure to delete ${book.title}`);
      if (result) {
        axios
          .delete(`http://localhost:3000/book/delete/${bookId}`)
          .then((response) => {
            alert(response.data + " Please refreah page");
          })
          
          .catch((err) => {
            console.log(err);
          });
          axios.get(`http://localhost:3000/`).then((response) => {
      console.log(response.data);
      this.books = response.data;
    });
      }
    },
    toCartPage() {
      const userId = this.user.user_id;
      this.$router.push(`/cart/${userId}`);
    },
    toHomePage() {
      const userId = this.user.user_id;
      this.$router.push(`/homePage/${userId}`);
    },
    onChange() {
      const data = { selected: this.selected };
      axios
        .post(`http://localhost:3000/book/selectType`, data)
        .then((response) => {
          this.books = response.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    toBillPage(){
      const userId = this.user.user_id
      this.$router.push(`/billPage/${userId}`)
    },
  },
};
</script>

<style>
.gdeletebutt {
  border: none;
  padding: 10px;
  font-size: 1.2rem;
  border-radius: 10px;
}

.gsetedit {
  position: absolute;
  top: 0;
  right: 0;
  width: 135px;
}
.geditbutt {
  border: none;
  padding: 10px;
  font-size: 1.2rem;
  border-radius: 10px;
  float: left;
}

body {
  background-color: #f2e0c3;
}

footer {
  background-color: #6d7352;
}

.g-navitem {
  font-size: 2rem;
  color: white;
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
  letter-spacing: 3px;
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
  letter-spacing: 15px;
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