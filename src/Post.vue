<template>
  <transition name="fade" appear>
    <div class="post" v-if="visible">
      <div class="post__header overlay">
        <img v-bind:src="post.img" alt="">
        <div class="header__content">
          <div class="panel__meta-data--left">
            <span class="panel__category">{{ post.category }}</span> / <span class="panel__date">{{ post.date }}</span>
          </div>
          <h2 class="panel__title">{{ post.title }}</h2>
          <p class="panel__desc">{{ post.desc }}</p>
        </div>
      </div>
      <div class="post__body">
        <div class="scroll-indicator-wrapper"><span class="scroll-indicator">Scroll</span></div>
        <div class="post__sidebar">
          <span class="post__category">{{ post.category }}</span> <span class="post__date">{{ post.date }}</span>
        </div>
        <div class="post__content">
          <p>The longhorn reared its enormous head and eyed me knowingly. 'Please don't charge,' I uttered politely. All the reassurance that had come with my authentic cowboy hat had shattered, and as the bull's legs began to start up, like a plane propeller kicking into life, i realised how dangeriously under qualified I was for this role.</p>
          <img src="./assets/peaks.jpg" alt="">
          <p>I was in Saskatchewan, traversing its unique landscape that coils from flat prairie in the south to rugged woodland in the north. The central Canadian province is (bar a few blemishes of white metropolis) like its flag: divided into two sections of green and gold.</p>
          <p>The immense landscape is all consuming, and hikers, horsemen, fishermen and adventurers travel from across the globe to lose themselves within it. Long before I’d witnessed the pull of a pike on a fishing rod or considered the extent of the damage a bull’s horn could do to a man’s internal organs, I’d felt the wilderness of the place.</p>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: ['visible', 'post'],
  data () {
    return {
      img: './src/assets/peaks.jpg',
      title: 'Exploring the Land of the Living Skies',
      category: 'Saskatchewan',
      date: '28.12.16',
      desc: 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. Dolorem natus repellat qui deleniti enim aspernatur consequuntur accusantium pariatur.'
    }
  }
}
</script>

<style lang="scss">
.fade-enter-active, .fade-leave-active {
  transition: visibility 15s;

  .panel__meta-data--left,
  .panel__meta-data--left:after,
  .panel__title,
  .panel__desc,
  .scroll-indicator {
    transition: transform 0.3s cubic-bezier(0.390, 0.575, 0.565, 1.000),
                opacity 0.3s cubic-bezier(0.390, 0.575, 0.565, 1.000);
  }
}

.fade-enter-active {
  .panel__meta-data--left {
    transition-delay: 0;
  }

  .panel__meta-data--left:after {
    transition-delay: 100ms;
  }

  .panel__title {
    transition-delay: 175ms;
  }

  .panel__desc {
    transition-delay: 225ms;
  }

  .scroll-indicator {
    transition-delay: 325ms;
  }
}

.fade-enter, .fade-leave-to {
  visibility: visible;;

  .panel__meta-data--left,
  .panel__meta-data--left:after,
  .panel__title,
  .panel__desc {
    opacity: 0;
    transform: translateY(40px);
  }

  .scroll-indicator {
    opacity: 0;
    transform: translateX(40px);
  }
}

.scroll-indicator-wrapper {
  position: absolute;
  transform: translateX(-50%) rotate(90deg);
  left: 50%;
  top: -10px;
  z-index: 2;
}

.scroll-indicator {
  font-family: 'Roboto';
  color: rgb(255,255,255);
  font-weight: 500;
  font-size: 0.9em;
  position: relative;
  display: inline-block;

  &:after {
    content: '';
    display: inline-block;
    width: 150px;
    height: 3px;
    background: #dba54b;
    vertical-align: middle;
    margin-left: 15px;
    margin-top: -3px;
  }
}

.post__header {
  height: 100vh;
  overflow: hidden;
}

.header__content {
  position: absolute;
  bottom: 5vw;
  left:  5vw;
  z-index: 3;
}

.post__header img {
  width: 100%;
  position: absolute;
  transform: scale(1.2)
}

.post__sidebar {
  font-family: 'Eczar';
  position: absolute;
  left: -5vw;
  top: 8vw;
  line-height: 1.65;
  letter-spacing: 0.05em;
  transform-origin: top left;
  transform: rotate(90deg);

  &:before {
    content: '';
    display: inline-block;
    width: 50px;
    height: 2px;
    background: #dba54b;
    vertical-align: middle;
    margin-right: 15px;
    margin-top: -3px;
  }
}

.post__category {
  font-weight: 500;
  margin-right: 15px;
}

.post__body {
  max-width: 1000px;
  position: relative;
  margin: 0 auto;
  color: #7e7e7e;
  padding-top: 8vw;
  padding-bottom: 8vw;
}

.post__content p {
  max-width: 60%;
  margin-left: auto;
  margin-right: auto;
  font-family: 'Eczar';
  font-size: 1.35em;
  line-height: 1.65;
}

.post__content img {
  max-width: 100%;
  display: block;
}

.post__content * + * {
  margin-top: 4vw;
}
</style>
