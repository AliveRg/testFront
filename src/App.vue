<script setup>
import iconImg from '@/components/icons/iconImg.vue'
import sceleton1 from '@/components/icons/sceleton_tit.vue'
import Grid from '@/components/Grid.vue'
</script>

<template>
  <div class="flex flex-col p-[32px] bg-[#1D1D1D] h-screen mx-auto">
    <div class="flex gap-[24px] items-center justify-center">
      <div
        class="flex flex-col items-center justify-center gap-[20px] px-[14px] pt-[18px] pb-[24px] border-[#4D4D4D] border-[1px] rounded-[8px] bg-[#262626]"
      >
        <iconImg>
          <img
            class="rounded-[8px] blur-[8px]"
            src="@/images/nicebg.png"
            alt=""
            style="width: 100%; height: 100%"
        /></iconImg>

        <sceleton1 />
      </div>
      <div
        class="relative flex flex-col items-center justify-center gap-[20px] border-[#4D4D4D] border-[0.5px] rounded-[8px] bg-[#262626] overflow-hidden"
      >
        <Grid />
      </div>
      <!-- <div class="flex items-center justify-center">
       
      </div> -->
    </div>

    <div class="w-full"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {}
  },
  components: {
    iconImg
  }
}
</script>

<style scoped></style>
