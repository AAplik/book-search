<!-- This component recieves books for App.vue and displays them -->
<script>
export default{
    props: ['books'],
    data() {
        return {
            showModal: false,
            title: "",
            author: "",
            year: "",
            pages: "",
            genre: [],
            image: "",
            description: "",
        }
    }, 
    methods: {
        fillModal(book){
            this.showModal = true
            this.title = book.title
            this.author = book.author
            this.year = book.year
            this.pages = book.pages
            this.genre = book.genre
            this.image = book.cover
            this.description = book.description
        }
    }
}
</script>

<template>

  <div class="box my-4" v-for="book in books">
  <article class="media">
        <figure class="media-left">
            <p class="image is-64x64 is-2by3">
                <img :src=book.cover>
            </p>
        </figure>
        <div class="media-content">
            <div class="content">
                <p>
                    <strong>{{ book.title }}</strong>
                    <br>
                    <small>{{ book.author }}</small>
                    <br>
                    <small>{{ book.year }}</small>
                    <br>
                    <button class="button is-info is-light is-small" @click="this.fillModal(book)">More Info</button>
                </p>
            </div>
        </div>
    </article>
    </div>

<!-- ----------------------------The Modal------------------------ -->
    <div id="modal-book-info" class="modal is-active" v-if="this.showModal">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
            <p class="modal-card-title">{{this.title}}</p>
            <button class="delete" aria-label="close" @click="this.showModal = false"></button>
            </header>
            <section class="modal-card-body">
                <!-- Content ... -->
                <div class="columns">
                    <div class="column">
                        
                        <figure class="image is-2by3">
                            <img :src=this.image>
                        </figure>
                    </div>
                    <div class="column">
                        <p class="title is-2">{{ this.title }}</p>
                        <p class="subtitle is-4">{{ this.author }}</p>
                        <div class="block">Published in {{ this.year }}</div>
                        <div class="block">{{ this.pages }} pages long</div>
                        <p class="subtitle is-5">Genres</p>
                        <div class="tags are-medium">
                        <span class="tag is-info is-rounded" v-for="genre in this.genre">{{ genre }}</span>
                        </div>
                    </div>
                </div>
                    <p class="subtitle is-5">Description</p>
                    <div class="block">{{ this.description }}</div>
            </section>
            <footer class="modal-card-foot">
            <button class="button" @click="this.showModal = false">Cancel</button>
            </footer>
        </div>
    </div>

</template>


<style>
</style>