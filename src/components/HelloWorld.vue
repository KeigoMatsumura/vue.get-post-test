<template>
  <div>
    <h2>Get</h2>
    <label>Name<input class="form-control" type="text" placeholder="name" v-model="name"/></label>
    <br/>
  
    <label>Age <input class="form-control" type="number" placeholder="age" v-model="age"/>
    </label>
  
    <br/>
    <!-- Exec button and show result -->
    <input class="btn btn-primary" type="button" value="Get" @click="execGet"/>
    {{ resGet }}
    

    <h2>Post</h2>
    <label>Description <input type="text" name="description" value="Hi! This is John."/></label>
    
    <br/>
    <!-- Exec button and show result -->
    <input class="btn btn-primary" type="button" value="Post" @click="execPost"/>
    {{ resPost }}

  </div>
</template>

<script>
export default {
data() {
 return {
   name: "David",
   age: 25,
   resGet: null,
   statusGet: 0,
 }
},
methods: {
 execGet() {
   let url = new URL("https://httpbin.org/get")

   let params = {
     name: this.name,
     age: this.age,
   }
   url.search = new URLSearchParams(params).toString()
   fetch(url)
     .then((response) => {
       this.statusGet = response.status
       return response.json()
     })
     .then((data) => {
       this.resGet = data
     })
 },
 execPost() {
     let url = new URL("https://httpbin.org/post")
     fetch(url, {
       method: "POST",
       body: this.description,
     })
       .then((response) => {
         this.statusPost = response.status
         return response.json()
       })
       .then((data) => {
         this.resPost = data
       })
   },
},
}
</script>