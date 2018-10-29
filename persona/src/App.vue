<template>
  <div id="app">
    <main>
      <section class="user-profile">
        <label class="user-avatar" for="files">
          <input type="file" id="files" name="files" class="avatar-btn" @change="uploadImg">
          <img :src="imgUrl" alt="アバター" class="avater-img">
        </label>

        <CardSingle placeholder="名前" maxlength="12" />
        <CardSingle placeholder="年齢" maxlength="2" />
        <CardMulti placeholder="職業、住まい、趣味など" rows="8" />
      </section>

      <section class="user-data">
        <CardMulti placeholder="ユーザーストーリー：どのような経歴・背景から、どのような日常生活やシチュエーションか" rows="8" />
        <CardMulti placeholder="課題：その日常生活で抱えている悩みごと" rows="8" />
        <CardMulti placeholder="ゴール：どうなりたいか、どんな目的があるか" rows="8" />
      </section>
    </main>

    <footer><img src="./assets/images/logo_black.svg" alt=""></footer>
  </div>
</template>

<script>
import CardSingle from './components/CardSingle.vue'
import CardMulti from './components/CardMulti.vue'

export default {
  name: 'app',
  components: {
    CardSingle, CardMulti
  },

  data () {
    return {
      imgUrl: require('./assets/images/avatar.png')
    }
  },

  methods: {
    uploadImg: function(evt){
      let files = evt.target.files; // inputタグからFileオブジェクトを取得
      let vm = this;

        let reader = new FileReader(); // ファイル読み取り用オブジェクト作成

        // ファイルを読み時
        reader.onload = (function(theFile) {
          return function(e) {
            vm.imgUrl = e.target.result;
          };
        })(files[0]);

        // データURLにエンコードした内容を格納
        reader.readAsDataURL(files[0]);
      // }
    }
  }
}
</script>

<style lang="scss">
/*
  Colors
*/
$gray: #f4f4f4;
$gray_l: #ccc;


/*
  Fonts
*/
$fontM : 16px;


/*
  Settings
*/
$unit: 4px;
@import url(//fonts.googleapis.com/earlyaccess/notosansjp.css);

* {
  box-sizing: border-box;
}

:placeholder-shown {
  color: $gray_l;
}

::-webkit-input-placeholder {
  color: $gray_l;
}

::-moz-placeholder {
  color: $gray_l;
}
:-ms-input-placeholder {
  color: $gray_l;
}


/*
  Styling
*/
body {
  background-color: $gray;
  margin: 0; padding: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Noto Sans JP", "ヒラギノ角ゴ ProN W3", "Hiragino Kaku Gothic ProN", "メイリオ", Meiryo, Verdana, sans-serif;
}

main {
  display: flex;
  width: 900px;
  margin: 0 auto;
  padding: ($unit * 10) 0;

  .user-profile {
    width: 240px;
    margin-right: 40px;

    .user-avatar {
      width: 240px;
      height: 240px;
      display: block;
      border-radius: 50%;
      overflow: hidden;
      margin: 0 auto ($unit * 5) auto;
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
    width: 620px;
  }

  .card {
    input[type="text"],textarea {
      background-color: #fff;
      border-radius: $unit * 2;
      padding: $unit * 4;
      border: none;
      outline: none;
      width: 100%;
      margin-bottom: $unit * 4;
      font-size: $fontM;
    }
  }
}

footer {
  text-align: center;
  margin: 0 0 ($unit * 10) 0;

  img {
    height: 24px;
  }
}

</style>
