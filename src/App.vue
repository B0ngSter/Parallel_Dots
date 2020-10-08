<template>
  <div id="app">
    <div class="profile">
      <img :src="profile.cover_pic" class="background"/>
      <img :src="profile.profile_pic" alt="photo" class="profile"/>
      <div class="name text-white">
        <h3>
          I am {{ profile.name }}
        <br>
          <small>{{ profile.designations }}</small>
        </h3>
      </div>
    </div>
    <!-- <p style="position: fixed;" class="text-white">
      {{ boo }}
      {{ pixel }}
    </p> -->
    <div class="text-white">
      <p>E-mail: <span>{{ profile.email }}</span></p>
      <p>Contact number: <span>{{ profile.contact }}</span></p>
      <p>Education: <span>{{ profile.education }}</span></p>
      <p>Skills: <span>{{ profile.skills }}</span></p>
      <p>Interests: <span>{{ profile.interests }}</span></p>
      <p>Work Experience: <span>{{ profile.experience }}</span></p>
      <p>Socials: 
      <span><a :href="profile.socials.insta"><img class="pl-4" alt="insta" src="./assets/social(1).svg"></a></span>
      <span><a :href="profile.socials.linkedin"><img class="pl-4" alt="linkedin" src="./assets/social(2).svg"></a></span>
      <span><a :href="profile.socials.fb"><img class="pl-4" alt="fb" src="./assets/social(3).svg"></a></span>
      </p>
    </div>
    <div class="blog text-white p-5">
      <h3>{{ profile.Project_types }}</h3>
      <div v-for="(project, idx) in profile.projects" :key="idx">
        <transition :name="transition(idx)" class="pl-5" >
        <b-card
          no-body
          class="text-center mt-5"
          v-if="boo.includes(idx)"
          :img-src="project.image_path"
          img-alt="Image"
          img-top
        >
        <a :href="project.link">
          <b-card-body>
            <b-card-title class="text-black">{{ project.title }}</b-card-title>
            <b-card-text class="text-black">
              {{ project.short_desprition }}
            </b-card-text>
          </b-card-body>
        </a>
        </b-card>
      </transition>
      </div>
    </div>
    <p class="text-white">Thank you</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      profile: {
        name: "John Doe",
        profile_pic: "https://tribune-reloaded.s3.amazonaws.com/media/images/1968527-fatthor-1557307837/1968527-fatthor-1557307837.jpg",
        cover_pic: "https://ca-times.brightspotcdn.com/dims4/default/444499c/2147483647/strip/true/crop/3000x2000+0+0/resize/840x560!/quality/90/?url=https%3A%2F%2Fcalifornia-times-brightspot.s3.amazonaws.com%2F7d%2F24%2F0d9fed4c40c285ffca41843ae569%2Fdecadefood.jpg",
        email: "XXXXXXX@gmail.com",
        contact: "+91XXXXXXXXX",
        education: "xxx, New Delhi",
        skills: "Blogging",
        interests: "foodie",
        experience: "X months",
        designations: "Blogger",
        socials: {
          insta: "https://www.instagram.com/nit35h_57/",
          fb: "https://www.facebook.com/Nit35H/",
          linkedin: "https://www.linkedin.com/in/nitesh-poonia-864549190/"
        },
        Project_types: "Blogs",
        projects: [
          {
            'title': "Punjabi food",
            'image_path': "https://www.shoutlo.com/uploads/articles/header-img-punjabi-delicacies.jpg",
            'short_desprition': "Okish",
            'link': ""
          },
          {
            'title': "Delhi Street food",
            'image_path': "https://media.tacdn.com/media/attractions-splice-spp-674x446/06/71/06/8e.jpg",
            'short_desprition': "yumm",
            'link': ""
          },
          {
            'title': "Rajasthani food",
            'image_path': "https://static.toiimg.com/photo/59108535.cms",
            'short_desprition': "superb",
            'link': ""
          },
          {
            'title': "Kerala food",
            'image_path': "https://edtimes.in/wp-content/uploads/2017/10/OnamSadya1-1.jpg",
            'short_desprition': "not cool",
            'link': ""
          },
          {
            'title': "Kashmiri food",
            'image_path': "https://mc.webpcache.epapr.in/mcms.php?size=large&in=https://mcmscache.epapr.in/post_images/website_266/post_9897253/thumb.jpg",
            'short_desprition': "Okish",
            'link': ""
          },
          {
            'title': "Bangali food",
            'image_path': "https://curlytales.com/wp-content/uploads/2019/10/images-5-5-1280x720.jpg",
            'short_desprition': "Okish",
            'link': ""
          }
        ]
      },
      // pixel: 0,
      boo: [],
    }
  },
  mounted() {
    document.addEventListener('scroll', this.scrollAnimation)
  },
  destroyed() {
    document.removeEventListener('scroll', this.scrollAnimation)
  },
  methods: {
    transition (idx) {
      if (idx%2 === 0) {
        return 'slide-fade-even'
      } else {
        return 'slide-fade-odd'
      }
    },
    scrollAnimation () {
      // this.pixel = document.documentElement.scrollTop
      const arr = [50, 400, 750, 1100, 1400, 1700, 2000, 2300]
      if (document.documentElement.scrollTop < 50) {
        this.boo = []
      }
      for ( var i = 0; i < arr.length; i++ ) {
        /* eslint-disable no-debugger */
        // debugger
        /* eslint-enable no-debugger */
        if (document.documentElement.scrollTop > arr[i]) {
          if (!this.boo.includes(i)) {
            this.boo.push(i)
          }
        }
      }
      if (document.documentElement.scrollTop < arr[this.boo[this.boo.length - 1]]) {
        this.boo.splice(this.boo.length - 1, 1)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body{
  margin: 0;
  background-color: #000000;
  padding: 0;
  max-width:100%;
}
.text-white {
  color: #ffffff;
}.text-black {
  color: #000000;
}
@media screen and (max-width: 500px) {
  .background{
    width:160%;
  }
}
.profile {
  font-family: 'Mansalva', cursive;
  position: relative;
  float: left;
  overflow: hidden;
  width: 100%;
  color: #ffffff;
  height: 70vh;
  text-align: center;
  border:none;
}
.profile .background {
  display:block;
  width:100%;
  height: 40vh;
  object-fit: cover;

}
.profile .name {
  width: 100%;
  padding: 15px 25px;
  position: absolute;
  left: 0;
  height: 100%;
  top: 70%;
}
.profile .profile {
  border-radius: 50%;
  position: absolute;
  bottom: 31%;
  left: 50%;
  width: 168px;
  height: 168px;
  max-width: 168px;
  opacity: 1;
  box-shadow: 3px 3px 20px rgba(0, 0, 0, 0.5);
  border: 2px solid rgba(255, 255, 255, 1);
  -webkit-transform: translate(-50%, 0%);
  transform: translate(-50%, 0%);
}
.slide-fade-even-enter-active {
  transition: all 1.3s ease-in;
}
.slide-fade-even-leave-active {
  transition: all 1.8s ease-in;
}
.slide-fade-even-enter, .slide-fade-even-leave-to {
  transform: translateX(-30px);
}
.slide-fade-odd-enter-active {
  transition: all 1.3s ease-in;
}
.slide-fade-odd-leave-active {
  transition: all 1.8s ease-in;
}
.slide-fade-odd-enter, .slide-fade-odd-leave-to {
  transform: translateX(30px);
}
</style>
