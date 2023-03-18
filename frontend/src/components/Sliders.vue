<template>
  <div class="slider">
    <div class="slides" :style="{ transform: `translateX(-${currentSlide * slideWidth}px)` }">
      <div v-for="(data, index) in campaigns" :key="index" class="slide">
        <div v-if="data.is_featured == 1" class="grid mb-5 p-5 sm:grid-cols-1 md:grid-cols-4 lg:grid-cols-4 gap-8">
          <div class="md:col-span-2 lg:col-span-1">
            <img class="pl-3 pt-3 pb-1 md:h-80 lg:h-56 sm:w-full md:w-96 lg:w-96" :src="data.campain_image" alt="Mountain"
              @click="donate(data.name)">
          </div>
          <div class="md:col-span-2 lg:col-span-3 pr-0 lg:pr-16">
            <button
              class="bg-[#364958] text-base rounded-lg pl-4 pr-4 pt-2 pb-2 text-white mb-2 md:mt-3">Featured</button>
            <h5 class="text-[#364958] text-2xl font-medium mb-2">{{ data.campaign_title }}</h5>
            <p class="text-[#364958]">
              {{ data.short_description }}
            </p>
            <button class="text-[#40b751] pt-3 font-bold" type="button" @click="donate(data.name)">Donate Now</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted, inject, provide, } from 'vue';
import axios from 'axios';

export default {
  name: 'Sliders',
  created() {
    this.get_campaigns()
  },
  props: {
    campaigns: {
      type: Array,
    },
    interval: {
      type: Number,
      default: 2000
    }
  },
  setup(props) {
    const currentSlide = ref(0);
    const slideWidth = ref(0);
    let timerId = null;

    const updateSlideWidth = () => {
      slideWidth.value = document.querySelector('.slider').offsetWidth;
    };

    const nextSlide = () => {
      currentSlide.value = (currentSlide.value + 1) % props.campaigns.length;
    };

    const startAutoPlay = () => {
      timerId = setInterval(nextSlide, props.interval);
    };

    const stopAutoPlay = () => {
      clearInterval(timerId);
    };

    onMounted(() => {
      updateSlideWidth();
      startAutoPlay();
    });

    onUnmounted(() => {
      stopAutoPlay();
    });

    return {
      currentSlide,
      slideWidth,
      updateSlideWidth
    };
  },
  data() {
    return {
      campaigns: []
    }
  },
  methods: {
    get_campaigns(category) {
      let url = ''
      if (category == null) {
        url = '/api/resource/Donation Campaign?filters={"published": 1}&fields=["name", "campain_image", "campaign_title", "is_featured","donation_amount", "raised_amount", "start_date", "end_date", "short_description", "ngo", "campaign_category"]'

      }
      else {
        url = `/api/resource/Donation%20Campaign?filters=[["Donation Campaign","campaign_category","=","${category}"],["Donation Campaign","published","=",1]]&fields=["name", "campain_image", "is_featured", "campaign_title", "donation_amount", "raised_amount", "start_date", "end_date", "short_description", "ngo", "campaign_category"]`

      }

      axios.get(url).then((response) => {
        console.log("campaign", response)
        this.campaigns = response.data['data']
      }).catch(function (error) {
        console.log(error);
      })
    },
  },
};
</script>

<style>
.slider {
  position: relative;
  overflow: hidden;
}

.slides {
  display: flex;
  transition: transform 0.3s ease-out;
}

.slide {
  flex: 0 0 100%;
}

img {
  width: 100%;
  height: auto;
}
</style>