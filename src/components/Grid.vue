<template>
  <div>
    <div
      class="absolute h-full bottom-0 top-0 right-0 w-1/2 z-10 bg-[#262626] border-l-[1px] border-l-[#4D4D4D] transition-all"
      :class="menu ? 'translate-x-[0]' : 'translate-x-[100%]'"
    >
      <button @click="closeMenu()" class="absolute top-2 right-2 text-white">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="12"
          height="12"
          viewBox="0 0 12 12"
          fill="none"
        >
          <path
            d="M12 1.05L10.95 0L6 4.95L1.05 0L0 1.05L4.95 6L0 10.95L1.05 12L6 7.05L10.95 12L12 10.95L7.05 6L12 1.05Z"
            fill="white"
          />
        </svg>
      </button>
      <transition name="fade">
        <div v-if="active" class="p-4">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="54"
            height="54"
            viewBox="0 0 54 54"
            fill="none"
          >
            <rect y="6" width="48" height="48" :fill="active.image2" />
            <g filter="url(#filter0_b_4412_10455)">
              <rect x="6" width="48" height="48" :fill="active.image" fill-opacity="0.35" />
            </g>
            <defs>
              <filter
                id="filter0_b_4412_10455"
                x="-6"
                y="-12"
                width="72"
                height="72"
                filterUnits="userSpaceOnUse"
                color-interpolation-filters="sRGB"
              >
                <feFlood flood-opacity="0" result="BackgroundImageFix" />
                <feGaussianBlur in="BackgroundImageFix" stdDeviation="6" />
                <feComposite
                  in2="SourceAlpha"
                  operator="in"
                  result="effect1_backgroundBlur_4412_10455"
                />
                <feBlend
                  mode="normal"
                  in="SourceGraphic"
                  in2="effect1_backgroundBlur_4412_10455"
                  result="shape"
                />
              </filter>
            </defs>
          </svg>

          <div class="mt-4" v-if="gridItems[active.id - 1]">
            <label class="block text-white mb-2">Введите количество</label>
            <input
              v-model="achivNumber"
              type="number"
              class="w-full px-2 py-1 border border-[#4D4D4D] bg-[#333] text-white"
            />
          </div>
          <div class="flex justify-end mt-4">
            <button @click="closeMenu()" class="px-4 py-2 bg-gray-500 text-white mr-2">
              Отмена
            </button>
            <button @click="closeSeveMenu(active.id)" class="px-4 py-2 bg-red-500 text-white">
              Подтвердить
            </button>
          </div>
          <button @click="deleteObj(active.id)" class="px-4 py-2 bg-red-500 text-white">
            Удалить
          </button>
        </div>
      </transition>
    </div>
    <div class="grid grid-cols-5 relative z-0">
      <div
        v-for="(item, index) in displayedItems"
        :key="index"
        :data-index="index"
        @click="addNewItem(index)"
        draggable="true"
        @dragstart="onDragStart($event, index)"
        @dragover="onDragOver($event)"
        @drop="onDrop($event, index)"
        class="relative flex items-center justify-center w-[100px] h-[100px] border-[#4D4D4D] border-[0.5px]"
      >
        <transition name="fade">
          <svg
            v-if="item.image"
            xmlns="http://www.w3.org/2000/svg"
            width="54"
            height="54"
            viewBox="0 0 54 54"
            fill="none"
          >
            <rect y="6" width="48" height="48" :fill="item.image2" />
            <g filter="url(#filter0_b_4412_10455)">
              <rect x="6" width="48" height="48" :fill="item.image" fill-opacity="0.35" />
            </g>
            <defs>
              <filter
                id="filter0_b_4412_10455"
                x="-6"
                y="-12"
                width="72"
                height="72"
                filterUnits="userSpaceOnUse"
                color-interpolation-filters="sRGB"
              >
                <feFlood flood-opacity="0" result="BackgroundImageFix" />
                <feGaussianBlur in="BackgroundImageFix" stdDeviation="6" />
                <feComposite
                  in2="SourceAlpha"
                  operator="in"
                  result="effect1_backgroundBlur_4412_10455"
                />
                <feBlend
                  mode="normal"
                  in="SourceGraphic"
                  in2="effect1_backgroundBlur_4412_10455"
                  result="shape"
                />
              </filter>
            </defs>
          </svg>
        </transition>
        <span
          v-if="item.number"
          class="absolute bottom-0 right-0 flex items-center justify-center h-[16px] w-[16px] rounded-tl-[6px] text-white border-[#4D4D4D] border-t-[1px] border-l-[1px] text-[10px]"
          >{{ item.number }}</span
        >
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Grid',
  data() {
    return {
      achivNumber: null,
      menu: false,
      active: {},
      maxItems: 25,
      gridItems: [],
      draggedItemIndex: null
    }
  },
  computed: {
    displayedItems() {
      return this.gridItems.slice(0, this.maxItems)
    }
  },
  created() {
    const savedItems = localStorage.getItem('gridItems')
    if (savedItems) {
      this.gridItems = JSON.parse(savedItems)
    } else {
      this.gridItems = [
        { id: 1, image: '#B8D998', image2: '#7FAA65', number: 4 },
        { id: 2, image: '#AA9765', image2: '#D9BB98', number: 2 },
        { id: 3, image: '#656CAA', image2: '#7481ED', number: 5 },
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {},
        {}
      ]
    }
  },
  watch: {
    gridItems: {
      handler(newGridItems) {
        localStorage.setItem('gridItems', JSON.stringify(newGridItems))
      },
      deep: true
    }
  },
  methods: {
    addNewItem(num) {
      if (this.gridItems[num].image) {
        this.openmenu(num)
      } else {
        const colors = ['#B8D998', '#AA9765', '#656CAA', '#7481ED']
        const randomColor1 = colors[Math.floor(Math.random() * colors.length)]
        const randomColor2 = colors[Math.floor(Math.random() * colors.length)]
        const randomNumber = 1

        this.gridItems[num] = {
          id: num,
          image: randomColor1,
          image2: randomColor2,
          number: randomNumber
        }

        if (this.gridItems.length > this.maxItems) {
          this.gridItems.pop()
        }
      }
    },
    openmenu(num) {
      if (this.active == this.gridItems[num]) {
        this.menu = false
        this.active = {}
        this.achivNumber = null
      } else {
        this.active = this.gridItems[num]
        this.achivNumber = this.gridItems[num].number

        this.menu = true
      }
    },
    closeMenu() {
      this.menu = false
      this.active = {}
    },
    closeSeveMenu(num) {
      function foundIndex(arr) {
        for (let i = 0; i < arr.length; i++) {
          const element = arr[i]
          if (element.id == num) {
            return i
          }
        }
      }

      this.gridItems[foundIndex(this.gridItems)].number = this.achivNumber
      this.menu = false
      this.active = {}
    },
    deleteObj(num) {
      function foundIndex(arr) {
        for (let i = 0; i < arr.length; i++) {
          const element = arr[i]
          if (element.id == num) {
            return i
          }
        }
      }

      this.gridItems[foundIndex(this.gridItems)] = {}
      this.menu = false
      this.active = {}
    },
    onDragStart(event, index) {
      this.draggedItemIndex = index
      event.dataTransfer.effectAllowed = 'move'
    },
    onDragOver(event) {
      event.preventDefault()
      event.dataTransfer.dropEffect = 'move'
    },
    onDrop(event, index) {
      event.preventDefault()
      if (this.draggedItemIndex !== null && this.draggedItemIndex !== index) {
        this.swapItems(this.draggedItemIndex, index)
      }
      this.draggedItemIndex = null
    },
    swapItems(fromIndex, toIndex) {
      const temp = this.gridItems[fromIndex]
      this.gridItems[fromIndex] = this.gridItems[toIndex]
      this.gridItems[toIndex] = temp
    }
  }
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
