<template>
  <div class="events">
    <div class="container">
      <div v-for="event in events" class="card">
        <div class="card-header">
          <img :src="(event.image)" alt="" srcset="" />
        </div>
        <div class="card-body">
          <h2>{{ event.name }}</h2>
          <p>{{ event.description }}</p>
        </div>
      </div>
      

      
    </div>
  </div>
</template>

<script>
import frame1 from '../assets/images/frame1.svg';
export default {
  name: "Events",
  data() {
    return {
      events: [
        {
          name: "Unleash Your Colors at Holi Land!",
          description:"Get ready for an explosion of color and fun at the Holi Land Color Festival! Join us for a vibrant celebration filled with music, dance, and the joyous tradition of throwing colorful powder. Let loose, connect with friends and strangers, and create unforgettable memories in a kaleidoscope of hues.",
          image: frame1,
        },
        {
          name: "Dance into a Rainbow at Holi Land Music Fest!",
          description:"Experience the ultimate Holi celebration with a musical twist at Holi Land Music Fest! Groove to the hottest beats spun by top DJs, surrounded by a sea of vibrant colors. This high-energy event combines the excitement of Holi with the thrill of a music festival, creating an electrifying atmosphere you won't want to miss.",
          image: frame1,
        },
        {
          name: "A Colorful Family Celebration at Holi Land!",
          description:"Bring the whole family for a day of colorful fun at Holi Land Family Fun Day! Enjoy a relaxed and joyful Holi celebration with kid-friendly activities, delicious food, and of course, plenty of colors to go around. Create lasting memories with your loved ones in a safe and festive environment, where laughter and smiles are guaranteed.",
          image: frame1,
        }
      ]
    };
  },
};
</script>

<style lang="css" scoped>
.events {
  width: 100%;
  color: #06195c;
}
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  justify-content: center;
  align-items: center;
  width: 100%;
}
.card {
  width: 300px;
  flex-grow: 1;
  margin-top: 2rem;
  border-radius: 10px;
  background-color: rgba(255, 255, 255, 0.425);
  backdrop-filter: blur(50%);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  animation: appear linear;
  animation-timeline: view();
  animation-range: entry 0% cover 40%;
}
.card-header {
  display: flex;
  justify-content: center;
}
.card-header img {
  width: 200px;
  height: 200px;
  margin: 1rem 0;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}
.card-body {
  padding: 1rem;
  text-align: center;
}
.card-body h2 {
  font-size: clamp(1.5rem, 2.5vw, 2rem);
  margin-bottom: 1rem;
}
.card-body p {
  font-size: clamp(1rem, 2vw, 1.25rem);
}


@media (max-width: 768px) {
  .container {
    flex-direction: column;
    gap: 0.5rem;
  }
  .card {
    width: 100%;
  }
  .card-header img {
    width: 100%;
    height: 200px;
  }
    
}

@keyframes appear {
    from {
        opacity: 0;
        scale: 0.5;
    }
    to {
        opacity: 1;
        scale: 1;
    }
}

</style>
