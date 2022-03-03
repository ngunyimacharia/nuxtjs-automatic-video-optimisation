<template>
<div class="my-10">
    <h1 class="text-center text-lg font-bold text-gray-700">Automatic video optimisation</h1>
    <h2 class="text-center text-md text-gray-600">Video by Monstera from Pexels</h2>
    <div class="mt-10 grid grid-cols-3">
      <div class="text-center p-3" v-for="quality in qualityOptions" :key="quality.value">
        <video class="mx-auto" :src="getVideoUrl(quality.value)" controls="false" autoplay="true" loop="true"/>
        <p class="text-md font-semibold p-3">Quality: {{quality.value}}</p>
        <p class="text-sm text-gray-500">{{quality.label}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      qualityOptions: [
        {
          label:"The optimal balance between file size and visual quality. By default, this is the same as q_auto:good.",
          value:"auto"
        },
        {
          label:"Less aggressive algorithm. Generates bigger files with potentially better visual quality.",
          value:"auto:best"
        },
        {
          label:"Ensuring a relatively small file size with good visual quality. Example of a target audience: stock media sites that display videos with a high visual quality.",
          value:"auto:good"
        },
        {
          label:"More aggressive algorithm, which results in smaller files of slightly lower visual quality. Example of a target audience: popular sites and social networks with a huge amount of traffic.",
          value:"auto:eco"
        },
        {
          label:"Most aggressive algorithm, which results in the smallest files of low visual quality. Example of a target audience: sites using thumbnail preview videos that then link to higher quality videos.",
          value:"auto:low"
        },
      ]
    };
  },
  methods:{
    getVideoUrl(quality){
      return this.$cloudinary.video
                .url(
                  'nuxtjs-automatic-video-optimisation/pexels-gabby-k-6915751', 
                  { 
                    quality ,
                    crop: 'fill', 
                    width: 300, 
                    height:300,
                    format: 'mp4'
                  }
                );
    }
  }
}
</script>
