<template>
   <div id="main" v-scroll="fetchDataOnScroll" class="d-flex flex-column flex-lg-row justify-center align-center flex-wrap">
     
    <v-card class="ma-2 " color="#26c6da" :min-width="cardWidth" ripple
      v-for="blog in blogs" :key="blog.id" @click="openDialog(blog.id)">
        <v-card-title>
          <v-icon large left>mdi-twitter </v-icon>
          <span class="title font-weight-light">{{blog.title.slice(0, 50)}}</span>
        </v-card-title>

        <v-divider light inset></v-divider>

        <v-card-text class="headline font-weight-bold">
          {{blog.body.slice(0,50)}}
        </v-card-text>

        <v-card-actions>
          <v-list-item class="grow">
            <v-list-item-content>
              <v-list-item-title>{{blog.userId}}</v-list-item-title>
            </v-list-item-content>

            <v-row align="center" justify="end" >
              <v-icon class="mr-1">mdi-heart</v-icon>
              <span class="subheading mr-2">{{blog.id}}</span>
            </v-row>
          </v-list-item>
        </v-card-actions>
     
    </v-card>
    <v-dialog v-model="dialog" width="600px">
      <v-card>
          <v-card-title>
              <span class="headline">{{singleBlog.title}}</span>
          </v-card-title>
          
          <v-card-text>{{singleBlog.content}}</v-card-text>

          <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="green darken-1" text @click="dialog = false">Close</v-btn>
          </v-card-actions>
      </v-card>
    </v-dialog>
   </div>

</template>

<script>


export default {
  data: function () {
    return {
      blogs: [],
      cardWidth: '',
      dialog: false,
      singleBlog: {
        title : "",
        content: ""
      },
    }
  },
  mounted(){
          this.fetchDataOnScroll(); 
          switch (this.$vuetify.breakpoint.name) {
            case 'xs': case 'sm': return this.cardWidth = '90%'
            case 'lg': case 'md': case"xl" : return this.cardWidth = '30%'
          }
  },
  methods: {
    openDialog: function(id){
      console.log("OpenDialog")
      this.blogs.forEach(blog => {
          if (blog.id == id){
            this.singleBlog.title = blog.title;
            this.singleBlog.content = blog.body;
            this.dialog = true;
          }
      });
    },
    fetchDataOnScroll: function(e){
        let scrollHeight = document.documentElement.scrollHeight;
        let scrollY = window.scrollY;
        let clientHeight = document.documentElement.clientHeight;
        
        if (Math.floor(scrollY + clientHeight) == scrollHeight){
          this.$axios.get('https://jsonplaceholder.typicode.com/posts')
                    .then((response) => {
                      response.data = response.data.slice(this.blogs.length, this.blogs.length + 10);
                      if (!response.data.length) this.$emit("hideProgress", false);
                      this.blogs = [...this.blogs, ...response.data];
                    })
                    .catch((error) => {
                      console.log(error);
                    })
          }
    }
  }

}
</script>
