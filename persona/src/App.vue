<template>
  <div id="app">
    <header><img src="./assets/images/logo_black.svg" alt=""></header>
    <main>
      <section class="user-profile">
        <label class="user-avatar" for="files">
          <input type="file" id="files" name="files" class="avatar-btn" @change="uploadImg">
          <img :src="imgUrl" alt="アバター" class="avater-img">
        </label>

        <input type="text" placeholder="名前" maxlength="12" v-model="name" @keyup="setStorage('name')" @change="setStorage('name')" />
        <input type="text" placeholder="年齢" maxlength="2" v-model="age" @keyup="setStorage('age')" @change="setStorage('age')" />
        <textarea placeholder="職業、住まい、趣味など" rows="8" v-model="profile" @keyup="setStorage('profile')" @change="setStorage('profile')" />
      </section>

      <section class="user-data">
        <textarea placeholder="ユーザーストーリー：どのような経歴・背景から、どのような日常生活やシチュエーションか" rows="8" v-model="story" @keyup="setStorage('story')" @change="setStorage('story')" />
        <textarea placeholder="課題：その日常生活で抱えている悩みごと" rows="8" v-model="issue" @keyup="setStorage('issue')" @change="setStorage('issue')" />
        <textarea placeholder="ゴール：どうなりたいか、どんな目的があるか" rows="8" v-model="goal" @keyup="setStorage('goal')" @change="setStorage('goal')" />
      </section>
    </main>
    <footer><small><a href="https://twitter.com/kyota" target="_blank">©kyota</a></small></footer>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      name: '',
      age: '',
      profile: '',
      story: '',
      issue: '',
      goal: '',
      imgUrl: require('./assets/images/avatar.png')
    }
  },

  mounted: function(){
    // ローカルストレージをセット
    for(let key in localStorage){
      this[key] = localStorage.getItem(key);
    }
  },

  methods: {
    uploadImg: function(evt){
      let files = evt.target.files; // inputタグからFileオブジェクトを取得
      let reader = new FileReader(); // ファイル読み取り用オブジェクト作成
      let vm = this;

        // ファイルを読み時
        reader.onload = (function(){
          return function(e){
            vm.imgUrl = e.target.result;
            vm.setStorage('imgUrl', vm.imgUrl);
          };
        })(files[0]);

        // データURLにエンコードした内容を格納
        reader.readAsDataURL(files[0]);
    },

    setStorage: function(key){
      localStorage.setItem(key, this[key]);
    }
  }
}
</script>

<style lang="scss">
/*
  Colors
*/
$gray-light: #f4f4f4;
$gray-normal: #ccc;
$blue: #1bb0cc;


/*
  Fonts
*/
$fontM: 16px;
$fontS: 12px;


/*
  Settings
*/
@import url(//fonts.googleapis.com/earlyaccess/notosansjp.css);

* {
  box-sizing: border-box;
}

:placeholder-shown {
  color: $gray-normal;
}

::-webkit-input-placeholder {
  color: $gray-normal;
}

::-moz-placeholder {
  color: $gray-normal;
}
:-ms-input-placeholder {
  color: $gray-normal;
}


/*
  Styling
*/
body {
  background-color: $gray-light;
  margin: 0; padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Noto Sans JP", "ヒラギノ角ゴ ProN W3", "Hiragino Kaku Gothic ProN", "メイリオ", Meiryo, Verdana, sans-serif;
}

header {
  text-align: center;
  margin: 24px 0;

  img {
    height: 24px;
  }
}

main {
  display: flex;
  width: 960px;
  margin: 0 auto;

  .user-profile {
    width: 240px;
    margin-right: 40px;

    .user-avatar {
      width: 240px;
      height: 240px;
      display: block;
      border-radius: 50%;
      overflow: hidden;
      margin: 0 auto 20px auto;
      cursor: pointer;

      .avatar-btn {
        display: none;
      }

      .avater-img {
        object-fit: cover;
        width: 100%;
        height: 100%
      }
    }
  }

  .user-data {
    width: 680px;
  }

  input[type="text"], textarea {
    background-color: #fff;
    border-radius: 8px;
    padding: 16px;
    border: none;
    outline: none;
    width: 100%;
    margin-bottom: 16px;
    font-size: $fontM;
    transition: all 300ms 0s ease-in;
  }

  input[type="text"]:focus, textarea:focus {
    box-shadow: 0px 0px 10px $blue;
  }

  textarea {
    resize: none;
  }
}

footer {
  text-align: center;
  font-size: $fontS;

  a {
    color: $blue;
    text-decoration: none;
  }

  a:hover {
    opacity: .5;
  }
}
</style>
