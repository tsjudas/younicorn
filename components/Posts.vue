<template>
  <div class="top flex-column center width-100">
    <div class="flex-column width-96 post-card" v-for="post in posts" :key="post.id">
      <div class="flex-row flex-start width-100">
        <i class="fas fa-tags"></i>
        <div class="spacer-width-small"></div>
        <p class="number-txt">{{post.category}}</p>
        <div class="spacer-width-var"></div>
        <i class="far fa-calendar"></i>
        <div class="spacer-width-small"></div>
        <p class="number-txt">{{parseDateStr(post.startTime)}}</p>
      </div>
      <div class="spacer-height-medium"></div>
      <div class="flex-row flex-start width-100 flex-wrap hidden-small">
        <span class="tag is-info has-margin" v-for="tag in getSplitedTags(post.tags)" :key="tag">
          {{tag}}
        </span>
      </div>
      <div class="spacer-height-medium"></div>
      <div class="flex-row flex-start width-100">
        <div class="img-container flex-row center">
          <img class="thumbnail" :src="post.thumbnail">
        </div>
      </div>
      <div class="spacer-height-medium"></div>
      <div class="flex-column width-100">
        <a :href="post.youtubeLink" target="_blank"><p class="bold title-txt black title-border">{{post.title}}</p></a>
      </div>
      <div class="spacer-height-medium"></div>
      <div class="flex-row flex-start width-100">
        <div class="flex-row center bold number-txt">
          <i class="far fa-clock"></i>
          <div class="spacer-width-small"></div>
          <p>{{getTimeStrBySec(post.length)}}</p>
        </div>
        <div class="spacer-width-large"></div>
        <div class="flex-row center bold number-txt">
          <i class="far fa-eye"></i>
          <div class="spacer-width-small"></div>
          <p>{{post.viewCnt.toLocaleString()}}</p>
        </div>
        <div class="spacer-width-large"></div>
        <a class="flex-row center link-img" :href="'https://nico.ms/' + post.contentId" target="_blank">
          <img src="niconico.png">
        </a>
        <div class="spacer-width-large"></div>
        <a class="flex-row center link-img" :href="post.youtubeLink" target="_blank">
          <img src="yt_icon_rgb.png">
        </a>
      </div>
      <div class="spacer-height-large"></div>
      <div class="cp_box">
        <input :id="'cp' + post.id" type="checkbox">
        <label :for="'cp' + post.id"></label>
        <div class="cp_container">
          <p v-html="post.description" class="info-txt"></p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.post-card {
  padding: 16px;
  box-shadow: 5px 5px 10px -6px gray;
  border: 1px solid lightgray;
  margin-bottom: 16px;
}
.img-container {
  max-width: 256px;
}
.thumbnail {
  height: 100%;
  width: 100%;
  object-fit: cover;
}
.title-txt {
  font-size: 20px;
  color: #5f5f5f;
}
.number-txt {
  font-size: 18px;
  color: #5f5f5f;
}
.info-txt {
  font-size: 12px;
}
.has-margin {
  margin-right: 8px;
  margin-bottom: 4px;
}
.flex-wrap {
  flex-wrap: wrap;
}
.title-border {
  border-bottom: 1px dotted black;
}
.link-img {
  width: 40px;
  height: 40px;
}
.spacer-width-var {
  width: 128px;
  height: 100%;
}

.cp_box *, .cp_box *:before, .cp_box *:after {
	-webkit-box-sizing: border-box;
	box-sizing: border-box;
}
.cp_box {
	position: relative;
}
.cp_box label {
	position: absolute;
	z-index: 1;
	bottom: 0;
	width: 100%;
	height: 100px; /* グラデーションの高さ */
	cursor: pointer;
	text-align: center;
	/* 以下グラデーションは背景を自身のサイトに合わせて設定してください */
	background: linear-gradient(to bottom, rgba(250, 252, 252, 0) 0%, rgba(250, 252, 252, 0.95) 90%);
}
.cp_box input:checked + label {
	background: inherit; /* 開いた時にグラデーションを消す */
}
.cp_box label:after {
	line-height: 2.5rem;
	position: absolute;
	z-index: 2;
	bottom: 20px;
	left: 50%;
	width: 16rem;
	content: '詳細を開く';
	transform: translate(-50%, 0);
	letter-spacing: 0.05em;
	color: #ffffff;
	border-radius: 20px;
	background-color: darkcyan;
}
.cp_box input {
	display: none;
}
.cp_box .cp_container {
	overflow: hidden;
	height: 120px; /* 開く前に見えている部分の高さ */
	transition: all 0.5s;
}
.cp_box input:checked + label {
	/* display: none; 閉じるボタンを消す場合解放 */
}
.cp_box input:checked + label:after {
	content: '閉じる';
}
.cp_box input:checked ~ .cp_container {
	height: auto;
	padding-bottom: 80px; /* 閉じるボタンのbottomからの位置 */
	transition: all 0.5s;
}

@media screen and (min-width: 768px) {
  .hidden-large {
    display: none;
  }
}
@media screen and (min-width: 441px) and (max-width: 767px) {
  .title-txt {
    font-size: 16px;
  }
  .number-txt {
    font-size: 12px;
  }
  .info-txt {
    font-size: 10px;
  }
  .spacer-width-var{
    width: 80px;
  }
  .hidden-large {
    display: none;
  }
}
@media screen and (max-width: 440px){
  .title-txt {
    font-size: 14px;
  }
  .number-txt {
    font-size: 12px;
  }
  .info-txt {
    font-size: 10px;
  }
  .hidden-small {
    display: none;
  }
  .spacer-width-var{
    width: 40px;
  }
  .link-img {
    width: 32px;
    height: 24px;
  }
}
</style>

<script>
export default {
  props: {
    posts:  {
      type: Array,
      required: true,
      default: [],
    }
  },
  methods: {
    getTimeStrBySec(seconds) {
      const h = seconds / 3600 | 0;
      const m = seconds % 3600 / 60 | 0;
      const s = seconds % 60;

      return `${this.leftZeroPadding(h, 2)}:${this.leftZeroPadding(m, 2)}:${this.leftZeroPadding(s, 2)}`;
    },
    getSplitedTags(tags) {
      return tags.split(" ");
    },
    parseDateStr(dateStr) {
      const date = new Date(dateStr);
      return `${date.getFullYear()}-${this.leftZeroPadding(date.getMonth() + 1, 2)}-${this.leftZeroPadding(date.getDate(), 2)} ${
        this.leftZeroPadding(date.getHours(), 2)}:${this.leftZeroPadding(date.getMinutes(), 2)}:${this.leftZeroPadding(date.getSeconds(), 2)}`
    },
    leftZeroPadding(str, length) {
      if (str.length === length) {
        return;
      }
      let zero = "";
      for (let i = 0; i < length - 1; i++) {
        zero += "0";
      }
      return (zero + str).slice(-1 * length)
    }
  }
}
</script>
