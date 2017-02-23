<template>
  <div id="app">
    <h1 class="page-title">Explore Canada.</h1>
    <div class="panels" v-if="!visible">
      <div class="panel overlay" v-for="post in posts" @click="loadPost(post)" v-bind:class="{
        'hide':post.hidden,
        'transition-out': animating && !post.active,
        'open': animating && post.active
        }">
        <img class="panel__background" v-bind:src="post.img" alt="">
        <div class="panel__content">
          <div class="panel__meta-data">
            <span class="panel__category">{{ post.category }}</span> / <span class="panel__date">{{ post.date }}</span>
          </div>
          <h2 class="panel__title">{{ post.title }}</h2>
          <p class="panel__desc">{{ post.desc }}</p>
        </div>
      </div>
    </div>
    <post :visible="visible" :post="activePost"></post>
  </div>
</template>

<script>
import Post from './components/Post.vue'

export default {
  name: 'app',
  components: {
    Post
  },
  data () {
    return {
      visible: false,
      animating: false,
      activePost: false,
      posts: [
        {
          img: 'static/peaks.jpg',
          category: 'Featured',
          date: '03.02.17',
          title: 'Canada was named the top country to travel to in 2017',
          desc: 'Lorem ipsum dolar sit amet consectetur adipisicing elit. Ducimus, quaerat.',
          active: false,
          hidden: false
        },
        {
          img: 'static/road.jpg',
          category: 'Future Travel',
          date: '21.01.17',
          title: 'The Explore Canada road trip',
          desc: 'Maecenas nec odio et ante tincidunt tempus. Donec vitae sapien ut libero venenatis',
          active: false,
          hidden: false
        },
        {
          img: 'static/valley.jpg',
          category: 'Saskatchewan',
          date: '28.12.16',
          title: 'Explore the Land of the Living Skies',
          desc: 'Maecnas tempus, tellus eget condimentum rhoncus, sem quam semper libero, sit amet.',
          active: false,
          hidden: false
        }
      ]
    }
  },
  methods: {
    loadPost (post) {
      post.active = !post.active
      this.activePost = post

      this.toggleAnimating().then(() => {
        this.hidePosts()
      })

      setTimeout(() => {
        this.visible = true
      }, 1000)
    },
    hidePosts () {
      this.posts.forEach((post) => {
        if (!post.active) {
          post.hidden = true
        } else {
          post.hidden = false
        }
      })
    },
    toggleAnimating () {
      this.animating = true
      return new Promise((resolve) => {
        setTimeout(() => {
          resolve()
        }, 200)
      })
    }
  }
}
</script>

<style lang="scss">
.page-title {
  position: absolute;
  top: 1em;
  left: 1em;
  z-index: 10;
  font-family: 'Eczar';
  color: rgb(255,255,255);
  font-size: 20px;
  letter-spacing: 0.1em;
  font-weight: 400;
}

.panel.transition-out {
  &:after {
    transform: translateX(101%);
    background: white;
    z-index: 100;
    opacity: 1;
  }
  transition: width 0.3s 0.4s cubic-bezier(0.390, 0.575, 0.565, 1.000),
              min-width 0.3s 0.4s cubic-bezier(0.390, 0.575, 0.565, 1.000);
}

.panel.hide:after {
  transition: transform 0.3s cubic-bezier(0.390, 0.575, 0.565, 1.000);
  transform: translateX(0%);
}

.panel.hide {
  width: 0%;
  min-width: 0%;
}

.panel.open .panel__content{
  opacity: 0;
  transform: translateY(100%);
}

.panel.open {
  width: 100% !important;

  // &:after {
    // opacity: 0 !important;
  // }
}


.panels {
  width: 100vw;
  height: 100vh;
  display: flex;
}

.panel__content {
  position: relative;
  z-index: 3;
  transform: translateY(75%);
  transition: transform 0.35s cubic-bezier(0.390, 0.575, 0.565, 1.000), opacity 0.35s cubic-bezier(0.390, 0.575, 0.565, 1.000);
}

.panel:hover .panel__content {
  // transform: translateY(50%);
}

.panel__title,
.panel__desc,
.panel__meta-data {
  max-width: 450px;
  margin: 0 auto;
}

.panel__desc,
.panel__meta-data {
  font-family: 'Roboto';
  font-weight: 300;
  color: rgb(255,255,255);
  letter-spacing: 0.045em;
  line-height: 1.6;
}

.panel__category {
  font-weight: 500;
}

.panel__meta-data {
  position: relative;
  padding-top: 1em;

  &:before {
    content: '';
    top: 0;
    position: absolute;
    width: 3em;
    left: 50%;
    transform: translateX(-50%);
    height: 3px;
    background: #dba54b;
  }
}

.panel__meta-data--left {
  @extend .panel__meta-data;

  &:before {
    left: 0;
    transform: translatex(0);
  }
}

.panel__title {
  margin-top: 0.5em;
  margin-bottom: 1em;
  font-family: 'Eczar';
  font-weight: 500;
  font-size: 42px;
  letter-spacing: 0.05em;
  line-height: 1.2;
  color: #ffffff;
}

.panel__background {
  position: absolute;
  z-index: -2;
  width: 100vw;
  height: 100vh;
  object-fit: cover;
  top: 0;
  transition: 0.5s 0.3s cubic-bezier(0.390, 0.575, 0.565, 1.000);
}


.panel.open .panel__background {
  transform: scale(1.2);
}

.panel:nth-child(2).open .panel__background {
  transform: translateX(-50vw) scale(1.2);
}

.panel:nth-child(1) .panel__background {
  left: 0;
}

.panel:nth-child(2) .panel__background {
  left: 50%;
  transform: translateX(-50vw);
}

.panel:nth-child(3) .panel__background {
  right: 0;
}

.panel {
  width: 33.333%;
  min-width: 550px;
  display: flex;
  align-content: center;
  justify-content: center;
  flex-direction: column;
  text-align: center;
  position: relative;
  overflow: hidden;
  transition: width 1s cubic-bezier(0.390, 0.575, 0.565, 1.000);


  &:after {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    // opacity: 0;
    transition: opacity 0.3s ease;
    z-index: -1;
  }

  &:after {
    // background: linear-gradient(to bottom, rgba(0,0,0,0), rgba(#dba54b,0.5));
    // opacity: 1;
  }

  &:hover {
    width: 100%;
    cursor: pointer;

    // &:before {
    //   opacity: 0;
    // }
    //
    // &:after {
    //   opacity: 1;
    // }
  }
}

.overlay {
  position: relative;

  &:before {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1;
    transition: opacity 0.3s ease;
    background: linear-gradient(to bottom, rgba(0,0,0,0), rgba(30,30,30, 0.6));
  }
}
</style>
