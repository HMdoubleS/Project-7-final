<template>
    <div class = "posts">
      <div :key="post.postid" class="card" >
        <div class="card-body">
            <i v-if="readCheck()" class="fas fa-envelope" type = "submit" id="unread" v-on:click ="addReadby()"></i>
            <h4 class="card-title"><strong>{{ post.title }}</strong></h4>
            <h5 class="card-subtitle mb-4 text-strong">posted by {{ post.author }}</h5>
            <p class="card-text mb-4">{{ post.posttext }}</p>
                <div class="card-img">
                  <img v-bind:src="post.image"/>
                </div>
            <p class="card-subtitle text-muted">{{ post.creationdate }}</p>
        </div>
      </div>  
    </div>
</template>

<script>
export default {
    data() {
      return {
        post: {}
      }
    },
    created() {
      this.getPost()
    },
    mounted() {
        this.readCheck()
    },
    methods: {   
        readCheck() {
            if (this.post.readby != null) {
                const check = this.post.readby.includes(JSON.parse(localStorage.getItem("user")).userId);
                console.log(check)
                return !check
            }
        },
        getImage() {
            return `/backend/images/${post.image}`
        },
        getPost() {
            let id = window.location.href.split('/').pop()
            const requestOptions = {
              method: "GET",
              headers: {
                  "Content-Type": "application/json",
                  Authorization: "Bearer " + JSON.parse(localStorage.getItem("user")).token,
              }, 
          }
          fetch("http://localhost:3000/api/posts/one/" + id, requestOptions)
            .then((res) => {
                return res.json()
            .then((data) => {
                this.post = data[0];
                console.log(data);
                });
            })
            .catch((error) => {
                console.error("There was an error!", error);
            });
        },
        addReadby() {
            let setReadby = []
            let userId = JSON.parse(localStorage.getItem("user")).userid
            let id = window.location.href.split('/').pop()
            console.log(id)
            if (JSON.parse(localStorage.getItem("user")).userid === this.userid) {
                setReadby = {
                    readby: userId,
                    postId: id
                }
            
            const requestOptions = {
                method: "PUT",
                headers: {
                    "Content-Type": "application/json",
                    Authorization: "Bearer " + JSON.parse(localStorage.getItem("user")).token,   
                }, 
                body: JSON.stringify(setReadby),
            };
            fetch("http://localhost:3000/api/posts/" + id,  requestOptions)
                .then((res) => {
                    return res.json()
                .then((data) => {
                    console.log(data);
                        if (res.ok) {
                            this.$router.push("/home");
                        }
                    });
                })
                .catch((error) => {
                    console.error("There was an error!", error);
                });
            }
        
        }
    }
}
</script>



<style scoped>

* {
    box-sizing: border-box;
    padding: 0;
    margin: 0;
}

.card {
    display: flex;
    flex-wrap: wrap;
    margin: 5rem 5rem 0 23rem;
    width: 45%;
    background: linear-gradient(to bottom right, #9ea5f4, #ffffff);
    box-shadow: 6px 6px 3px rgba(65, 64, 64, 0.867);
}

i {
    display: inline-block;
    position: absolute;
    margin-left: 85%;
    padding: .5rem;
}

.card-body {
    padding: 2rem;
}

img {
    height: auto;
    width: 100%;
    margin: .5rem;
    object-fit: cover;
}

@media screen and (max-width: 768px) {
    .card {
        display: flex;
        justify-content: center;
        margin: .5rem;
        width: 95%;
        box-shadow: none;
    }

    i {
        margin-left: 75%;
        padding: 0;
    }
}
</style>