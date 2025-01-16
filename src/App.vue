<script setup>
  import { ref, onMounted, isProxy, toRaw} from "vue";
  const isSortAndViewOpened = ref(false)
  const sortType = ref('new')
  const viewType = ref('list')
  const text = 'Hello World'
</script>

<template>
  <div class="w-full max-w-4xl flex flex-col items-center gap-4">
    <div class="flex flex-row gap-2 w-full text-blue-100 items-center border-emerald-900 border-2 px-4 py-2 rounded-xl">
      <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path class="fill-blue-100" fill-rule="evenodd" clip-rule="evenodd" d="M15.62 17.03C13.8231 18.4665 11.5443 19.1604 9.25178 18.969C6.95923 18.7777 4.82698 17.7158 3.29301 16.0013C1.75905 14.2869 0.939847 12.0501 1.00368 9.75048C1.06752 7.45085 2.00955 5.26297 3.63626 3.63626C5.26297 2.00955 7.45085 1.06752 9.75048 1.00368C12.0501 0.939847 14.2869 1.75905 16.0013 3.29301C17.7158 4.82698 18.7777 6.95923 18.969 9.25178C19.1604 11.5443 18.4665 13.8231 17.03 15.62L21.71 20.29C21.8032 20.3832 21.8772 20.4939 21.9277 20.6158C21.9781 20.7376 22.0041 20.8681 22.0041 21C22.0041 21.1319 21.9781 21.2624 21.9277 21.3843C21.8772 21.5061 21.8032 21.6168 21.71 21.71C21.6168 21.8032 21.5061 21.8772 21.3843 21.9277C21.2624 21.9781 21.1319 22.0041 21 22.0041C20.8681 22.0041 20.7376 21.9781 20.6158 21.9277C20.4939 21.8772 20.3832 21.8032 20.29 21.71L15.62 17.03ZM17 10C17 10.9193 16.8189 11.8295 16.4672 12.6788C16.1154 13.5281 15.5998 14.2997 14.9498 14.9498C14.2997 15.5998 13.5281 16.1154 12.6788 16.4672C11.8295 16.8189 10.9193 17 10 17C9.08075 17 8.1705 16.8189 7.32122 16.4672C6.47194 16.1154 5.70027 15.5998 5.05026 14.9498C4.40025 14.2997 3.88463 13.5281 3.53285 12.6788C3.18107 11.8295 3.00001 10.9193 3.00001 10C3.00001 8.14349 3.73751 6.36301 5.05026 5.05026C6.36301 3.73751 8.14349 3.00001 10 3.00001C11.8565 3.00001 13.637 3.73751 14.9498 5.05026C16.2625 6.36301 17 8.14349 17 10Z"/>
      </svg>
      <input class="w-full bg-transparent no-drag" type="text" placeholder="Search here...">
      <div class="flex flex-row items-center gap-2 no-drag cursor-pointer no-drag px-4 py-2 bg-emerald-900 hover:bg-emerald-950 transition-colors duration-700 rounded-3xl font-bold">
        <svg class="w-4 h-4 no-drag cursor-pointer" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path class="fill-blue-100" fill-rule="evenodd" clip-rule="evenodd" d="M12 23C14.9174 23 17.7153 21.8411 19.7782 19.7782C21.8411 17.7153 23 14.9174 23 12C23 9.08262 21.8411 6.28473 19.7782 4.22183C17.7153 2.15893 14.9174 1 12 1C9.08262 1 6.28473 2.15893 4.22183 4.22183C2.15893 6.28473 1 9.08262 1 12C1 14.9174 2.15893 17.7153 4.22183 19.7782C6.28473 21.8411 9.08262 23 12 23ZM12 6C12.2652 6 12.5196 6.10536 12.7071 6.29289C12.8946 6.48043 13 6.73478 13 7V11H17C17.2652 11 17.5196 11.1054 17.7071 11.2929C17.8946 11.4804 18 11.7348 18 12C18 12.2652 17.8946 12.5196 17.7071 12.7071C17.5196 12.8946 17.2652 13 17 13H13V17C13 17.2652 12.8946 17.5196 12.7071 17.7071C12.5196 17.8946 12.2652 18 12 18C11.7348 18 11.4804 17.8946 11.2929 17.7071C11.1054 17.5196 11 17.2652 11 17V13H7C6.73478 13 6.48043 12.8946 6.29289 12.7071C6.10536 12.5196 6 12.2652 6 12C6 11.7348 6.10536 11.4804 6.29289 11.2929C6.48043 11.1054 6.73478 11 7 11H11V7C11 6.73478 11.1054 6.48043 11.2929 6.29289C11.4804 6.10536 11.7348 6 12 6Z"/>
        </svg>
        <div class="no-drag cursor-pointer text-nowrap">
          Add
        </div>
      </div>
    </div>
    <div class="flex flex-row items-center w-full gap-4 pt-2 no-drag text-blue-100">
      <div @click="isSortAndViewOpened=!isSortAndViewOpened" class="flex flex-row gap-2 items-center bg-emerald-950 px-4 cursor-pointer py-1.5 rounded-2xl no-drag">
        <svg class="w-3 h-3 no-drag" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path class="fill-blue-100" d="M16.3 21.7C16.4869 21.8832 16.7383 21.9859 17 21.9859C17.2618 21.9859 17.5131 21.8832 17.7 21.7L21.7 17.7C21.8444 17.5074 21.9146 17.2692 21.8975 17.0291C21.8804 16.789 21.7773 16.5631 21.6071 16.3929C21.4369 16.2227 21.211 16.1196 20.9709 16.1025C20.7308 16.0855 20.4926 16.1556 20.3 16.3L18 18.58V3C18 2.73478 17.8947 2.48043 17.7071 2.29289C17.5196 2.10536 17.2652 2 17 2C16.7348 2 16.4804 2.10536 16.2929 2.29289C16.1054 2.48043 16 2.73478 16 3V18.59L13.7 16.29C13.5076 16.1274 13.2608 16.0435 13.0092 16.055C12.7575 16.0664 12.5195 16.1725 12.3426 16.3519C12.1657 16.5312 12.0631 16.7708 12.0552 17.0226C12.0473 17.2744 12.1347 17.5199 12.3 17.71L16.3 21.71V21.7ZM6.30001 2.3C6.48694 2.11677 6.73825 2.01414 7.00001 2.01414C7.26176 2.01414 7.51308 2.11677 7.70001 2.3L11.7 6.3C11.8444 6.49257 11.9146 6.73078 11.8975 6.97089C11.8804 7.211 11.7773 7.4369 11.6071 7.60711C11.4369 7.77732 11.211 7.88042 10.9709 7.89748C10.7308 7.91455 10.4926 7.84443 10.3 7.7L8.00001 5.42V21C8.00001 21.2652 7.89465 21.5196 7.70711 21.7071C7.51958 21.8946 7.26522 22 7.00001 22C6.73479 22 6.48044 21.8946 6.2929 21.7071C6.10536 21.5196 6.00001 21.2652 6.00001 21V5.41L3.70001 7.71C3.50756 7.87256 3.26084 7.9565 3.00918 7.94504C2.75752 7.93357 2.51947 7.82754 2.3426 7.64815C2.16573 7.46875 2.06309 7.22922 2.05519 6.97742C2.0473 6.72562 2.13473 6.48012 2.30001 6.29L6.30001 2.29V2.3Z"/>
        </svg>
        <div class="text-nowrap no-drag select-none">
          Sorting and view
        </div>
        <svg v-if="isSortAndViewOpened" class="w-5 h-5 no-drag" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path class="fill-blue-100" d="M5.30001 14.7C5.48694 14.8832 5.73826 14.9858 6.00001 14.9858C6.26176 14.9858 6.51308 14.8832 6.70001 14.7L12 9.41999L17.3 14.72C17.4925 14.8826 17.7392 14.9665 17.9908 14.955C18.2425 14.9436 18.4805 14.8375 18.6574 14.6581C18.8343 14.4787 18.9369 14.2392 18.9448 13.9874C18.9527 13.7356 18.8653 13.4901 18.7 13.3L12.7 7.29999C12.5131 7.11676 12.2618 7.01413 12 7.01413C11.7383 7.01413 11.4869 7.11676 11.3 7.29999L5.30001 13.3C5.20628 13.3929 5.13189 13.5036 5.08112 13.6254C5.03035 13.7473 5.00421 13.878 5.00421 14.01C5.00421 14.142 5.03035 14.2727 5.08112 14.3946C5.13189 14.5164 5.20628 14.627 5.30001 14.72V14.7Z"/>
        </svg>
        <svg v-else class="w-5 h-5 no-drag" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path class="fill-blue-100" d="M5.29999 9.3C5.48692 9.11678 5.73824 9.01415 5.99999 9.01415C6.26175 9.01415 6.51307 9.11678 6.69999 9.3L12 14.59L17.3 9.29C17.3904 9.18601 17.5013 9.10182 17.6258 9.04272C17.7503 8.98362 17.8856 8.95089 18.0233 8.94657C18.1611 8.94225 18.2982 8.96644 18.4261 9.01762C18.5541 9.06881 18.6701 9.14588 18.7668 9.244C18.8635 9.34213 18.939 9.45918 18.9883 9.58783C19.0377 9.71648 19.0599 9.85394 19.0537 9.9916C19.0474 10.1292 19.0127 10.2641 18.9519 10.3877C18.891 10.5114 18.8053 10.6211 18.7 10.71L12.7 16.71C12.5131 16.8932 12.2617 16.9959 12 16.9959C11.7382 16.9959 11.4869 16.8932 11.3 16.71L5.29999 10.71C5.20627 10.617 5.13187 10.5064 5.0811 10.3846C5.03033 10.2627 5.0042 10.132 5.0042 10C5.0042 9.86799 5.03033 9.73729 5.0811 9.61543C5.13187 9.49357 5.20627 9.38297 5.29999 9.29V9.3Z"/>
        </svg>
        <div v-if="isSortAndViewOpened" class="z-10 absolute top-40 ">
          <div class="bg-emerald-950 px-1.5 py-2 rounded-md">
            <div>
              <div class="font-semibold px-1.5 pb-1">Sort by</div>
              <div class="font-thin gap-1.5">
                <div @click="sortType='abc'" :class="`${sortType == 'abc'? 'underline': ''} cursor-pointer px-1.5 no-drag py-1 hover:bg-emerald-800 hover:text-blue-50 rounded`">Alphabetically</div>
                <div @click="sortType='new'" :class="`${sortType == 'new'? 'underline': ''} cursor-pointer px-1.5 no-drag py-1 hover:bg-emerald-800 hover:text-blue-50 rounded`">New ones first</div>
                <div @click="sortType='old'" :class="`${sortType == 'old'? 'underline': ''} cursor-pointer px-1.5 no-drag py-1 hover:bg-emerald-800 hover:text-blue-50 rounded`">First the old</div>
              </div>
            </div>
            <hr class="my-2 border-emerald-900">
            <div>
              <div class="font-semibold px-1.5 pb-1">View like</div>
              <div class="font-thin gap-1.5">
                <div @click="viewType='list'" :class="`${viewType == 'list'? 'underline': ''} cursor-pointer px-1.5 no-drag py-1 hover:bg-emerald-800 hover:text-blue-50 rounded`">List</div>
                <div @click="viewType='gallery'" :class="`${viewType == 'gallery'? 'underline': ''} cursor-pointer px-1.5 no-drag py-1 hover:bg-emerald-800 hover:text-blue-50 rounded`">Gallery</div>
                <div @click="viewType='feed'" :class="`${viewType == 'feed'? 'underline': ''} cursor-pointer px-1.5 no-drag py-1 hover:bg-emerald-800 hover:text-blue-50 rounded`">Feed posts</div>
              </div>
            </div>
            <hr class="my-2 border-emerald-900">
            <div @click="viewType='list';sortType='new'" class="cursor-pointer px-1.5 no-drag py-1 hover:bg-emerald-800 hover:text-blue-50 rounded text-emerald-500 ">
              Restore to default
            </div>
            
          </div>
        </div>
      </div>
      <div class="text-emerald-900 select-none">|</div>
      <div class="w-full overflow-y-auto flex flex-row gap-2 no-drag">
        <div class="no-drag cursor-pointer select-none">tags</div>
        <div class="no-drag cursor-pointer select-none">tags</div>
        <div class="no-drag cursor-pointer select-none">tags</div>
        <div class="no-drag cursor-pointer select-none">tags</div>
        <div class="no-drag cursor-pointer select-none">tags</div>
        <div class="no-drag cursor-pointer select-none">tags</div>
        <div class="no-drag cursor-pointer select-none">tags</div>
        <div class="no-drag cursor-pointer select-none">tags</div>
      </div>
    </div>
    <h1 class="text-blue-100">💖 {{text}}!</h1>
  </div>
</template>