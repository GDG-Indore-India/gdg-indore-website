<template>
    <!-- <v-list three-line subheader class="py-0" :class="$vuetify.theme.dark == true?'black':'white'">
        <v-list-item
        class=""
        @click="goToTeam(data.id)"
        >
            <v-list-item-avatar>
                <img :src="getImgUrl(data.image, 'profile.jpg')">
            </v-list-item-avatar>

            <v-list-item-content>
                <v-list-item-title class="google-font mb-0" v-text="data.name"></v-list-item-title>
                <v-list-item-subtitle class="google-font mb-0 mt-0" >{{ data.designation }}</v-list-item-subtitle>
                <socialMediaDetails class="pl-0 ml-0" :data="data.socialLinks"/>
            </v-list-item-content>
        </v-list-item> -->

        <!-- <v-divider inset></v-divider> -->
    <!-- </v-list> -->
     <v-dialog
      v-model="dialog"
      width="700"
    >
      <template v-slot:activator="{ on }">
          <div v-on="on" style="cursor: pointer;" class="text-center py-5 ma-1 fill-height" :class="$vuetify.theme.dark == true?'darkModeCard':'whiteTheme'" >
               <v-avatar size="100">
                  <img 
                    :src="getImgUrl(data.image, 'profile.jpg')"
                    :lazy-src="getImgUrl(data.image, 'profile.jpg')" alt=""
                  >
                </v-avatar>
                <p class="mt-3 mb-0 google-font mb-0" style="font-size:120%">{{data.name | summery(20)}}</p>
                <p class="mt-1 mb-0 google-font mt-0" style="font-size:80%">{{data.designation | summery(20)}}</p>
                <socialMediaDetails :data="data.socialLinks"/>
          </div>
      </template>

      <v-card :class="theme.isDark?'grey darken-3':'white'">
        <v-card-title
          class="px-5 google-font"
          primary-title
        >
         {{data.name}} 
        </v-card-title>

        <v-card-text class="pa-5">
            <p class="google-font">{{data.designation}}</p>
            <p class="google-font">{{data.bio}}</p>
            
            <socialMediaDetails  class="pl-0 ml-0" :data="data.socialLinks"/>

            <v-btn class="primary mt-3" small depressed @click="goToTeam(data.id)">See More Info</v-btn>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
</template>

<script>
    import socialMediaDetails from '@/components/common/SocialInfo'
  export default {
    inject: ['theme'],
    props:['data'],
    components:{
        socialMediaDetails
    },
    data () {
      return {
        dialog: false,
      }
    },
    methods:{
      goToTeam(id){
        this.$router.push("/team/" + id);
      },
    },
    filters:{
         summery: (val,num)=>{
            return val.substring(0,num)+".."
        },
        dateFilter: value => {
            const date = new Date(value);
            return date.toLocaleString(["en-US"], {
                month: "short",
                day: "2-digit",
                year: "numeric"
            });
        }
    }
  }
</script>
