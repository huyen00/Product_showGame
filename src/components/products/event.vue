<template>
  <div>

    <div class="menu_tab fixed z-30">
      <ul class="justify-center flex p-3.5 tab">
        <li class="mx-4">
          <button
            class="block"
            :class="tab =='official' ? 'text-orange-500' : ''"
            @click="showTab('official')"
          >
            <font-awesome-icon
              icon="fa-regular fa-clock"
              class="block mx-auto"
            />
            <span class="uppercase mt-2 text-md">official</span>
          </button>
        </li>
        <li class="mx-4">
          <button
            class="block"
            :class="tab =='Soon' ? 'text-orange-500' : ''"
            @click="showTab('Soon')"
          >
            <font-awesome-icon
              icon="fa-regular fa-clock"
              class="block mx-auto"
            />
            <span class="uppercase mt-2 text-md">Soon</span>
          </button>
        </li>
        <li class="mx-4">
          <button
            class="block"
            :class="tab =='Popular' ? 'text-orange-500' : ''"
            @click="showTab('Popular')"
          >
            <font-awesome-icon icon="fa-solid fa-users" class="block mx-auto" />
            <span class="uppercase mt-2 text-md">popular</span>
          </button>
        </li>
      </ul>
    </div>
    <div class="container mx-auto z-0">
      <div class="content_tab pt-16">
        <div
          class="content1"
        
          id="tabs-home"
          role="tabpanel"
          aria-labelledby="tabs-home-tab"
          data-te-tab-active
        >
          <div class="grid grid-cols-3 gap-4" >
            <div class="item_event" v-for="(item, index) in eventByCategory" :key="index">
              <div >
                <div class="p-4 flex">
                  <img :src="item.avata_event" class="rounded-full avata_event" alt="" />
                  <div class="ml-4">
                    <h2 class="text-md font-bold block">
                      {{ item.name_event }}
                    </h2>
                    <a href="" class="text-sm text-gray-500">{{
                      item.email_event
                    }}</a>
                  </div>
                </div>
                <div class="relative transform transition duration-500 group hover:scale-100 item_image" >
                  <img
                    :src="item.image_event"
                    class="w-full h-full object-cover"
                    alt=""
                  />
                  <div class="absolute top-0 item_text content_form overflow-hidden h-full w-full p-3 opacity-0 group-hover:opacity-100 bg-opacity-25" >
                    <div class="top-0 h-full overflow-auto scrollbar scrollbar-thumb-gray-400 scrollbar-track-gray-200" >
                      <span class="text-sm text-white">{{
                        item.content_event
                      }}</span>
                    </div>
                  </div>
                </div>
                <div class="p-2">
                  <span class="text-xs text-gray-500">{{
                    item.time_event
                  }}</span>
                  <p class="uppercase text-xs">
                    {{ item.member_event }} ATTENDING
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      
      </div>
    </div>
  </div>
</template>
<script>
import { mapState } from "vuex";
export default {
  name: "eventRoom",
  components: {
    // itemEvent,
  },
  computed: {
    tab(){
      return this.$store.state.stores.tab
    },  
    tab1() {
      return this.$store.state.stores.tab1;
    },
    tab2() {
      return this.$store.state.stores.tab2;
    },
    tab3() {
      return this.$store.state.stores.tab3;
    },
    ...mapState("stores", {
      events: (state) => state.events,
    }),

    eventByCategory(){
            return this.$store.getters['stores/eventByCategory']
    }
  },

  mounted() {
    this.$store.dispatch("stores/getEvent").then((response) => {
      console.log(response);
      this.$store.commit("stores/SET_EVENT", response.data);
    });
  },
  methods: {
    showTab(name){
      this.$store.commit('stores/showTab', name)

    },

  },
};
</script>

<style scoped>
.menu_tab {
  margin-top: -2.1rem;
  background: #fff;
  width: 100%;
  margin-left: -3rem;
  box-shadow: rgba(0, 0, 0, 0.45) 0px 25px 20px -20px;
}
.tab {
  padding: 0.9rem;
  margin-right: 12rem;
}
.container {
  max-width: 1080px;
}
.item_event {
  box-shadow: rgba(9, 30, 66, 0.25) 0px 4px 8px -2px,
    rgba(9, 30, 66, 0.08) 0px 0px 0px 1px;
}
.item_text {
  background: #00000087;
}
.avata_event{
  width: 40px;
  height: 40px;
}
.item_image{
  height: 350px;
}
</style>