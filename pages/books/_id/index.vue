<template>
    <!-- TODO: component化 Card -->
    <div class="card">
        <div class="card-image">
            <figure class="image">
            <img class="main-image" :src="imageURL" :alt="book.Title">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-left">
                    <figure class="image is-48x48">
                    <b-icon
                        icon="view-dashboard"
                        size="is-large"
                        type="is-primary">
                    </b-icon>
                    </figure>
                </div>
                <div class="media-content">
                    <div>
                        <p class="title is-4">{{ book.Title }}</p>
                        <p class="subtitle is-6">ISBN: {{ book.ISBN }}</p>
                    </div>
                    <div>
                        <nuxt-link :to="bookURL"><button class="button is-primary">EDIT</button></nuxt-link>
                        <nuxt-link to="/books">
                            <button @click="sendDeleteRequest" class="button is-primary">DELETE</button>
                        </nuxt-link>
                    </div>        
                </div>
            </div>

            <div class="content">
                <p>{{ book.Description }}</p>
                <time>{{ date }}</time>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    async asyncData({ app ,route }) {
        const response = await app.$axios.$get(`https://my-go-app-259011.appspot.com/api/v1/books/${route.params.id}`);
        return { 
            book: response,
            bookURL: response.ID + "/edit",
            date: new Date(),
            imageURL: `http://images-jp.amazon.com/images/P/${response.ISBN}.09.LZZZZZZZ`
        };
    },
    methods: {
        sendDeleteRequest() {
            const res = this.$axios.$delete(`https://my-go-app-259011.appspot.com/api/v1/books/${this.$route.params.id}`)
            .then((res) => {
                console.log(res)
            })
            .catch(err => console.error(err))
        }
    },
    created: function() {
        this.date = this.date.getFullYear(this.book.CreatedAt) + "年" + ( this.date.getMonth(this.book.CreatedAt) + 1 ) + "月" + this.date.getDate(this.book.CreatedAt) + "日"
        if (!this.book.ISBN) {
            this.imageURL = "https://bulma.io/images/placeholders/1280x960.png"
        }
    }
}
</script>
<style scoped>
    .main-image{
        max-height: 500px;
        height: 100%;
        width: auto;
        margin: 0 auto;
    }
    .card{
        width: 70%;
        margin: 0 auto;
    }
    .card-content{
        padding: 5%;
    }
    .media-content{
        display: flex;
        justify-content: space-between;
    }
    time{
        position: absolute;
        right: 5%;
    }
    .content{
        min-height: 100px; 
    }
</style>