<template>
  <div class="container">
    <div class="columns is-multiline">
      <div class="column is-12">
        <h1 class="title">Add MBTI</h1>
      </div>

      <div class="column is-12">
        <form @submit.prevent="submitForm" enctype="multipart/form-data">

          <div class="field">
            <label>board</label>
            <div class="control">
              <select class="select" v-model="board">
                <option value="상대법">상대법</option>
                <option value="주의할 점">주의할 점</option>
                <option value="특징">특징</option>
              </select>
            </div>
          </div>


          <div class="field">
            <label>MBTI</label>
            <div class="control">
              <select class="select" v-model="mbti">
                <option value="INFP">INFP</option>
                <option value="ENFP">ENFP</option>
                <option value="ESFJ">ESFJ</option>
                <option value="ISFJ">ISFJ</option>
                <option value="ISFP">ISFP</option>
                <option value="ESFP">ESFP</option>
                <option value="INTP">INTP</option>
                <option value="INFJ">INFJ</option>
                <option value="ENFJ">ENFJ</option>
                <option value="ENTP">ENTP</option>
                <option value="ESTJ">ESTJ</option>
                <option value="ISTJ">ISTJ</option>
                <option value="INTJ">INTJ</option>
                <option value="ISTP">ISTP</option>
                <option value="ESTP">ESTP</option>
                <option value="ENTJ">ENTJ</option>
              </select>
            </div>
          </div>

          <div class="field">
            <label>title</label>
            <div class="control">
              <input type="text" class="input" v-model="title">
            </div>
          </div>

          <div class="field">
            <label>Image</label>
            <input @change="mbtiImage()" type="file" ref="mbtiimage">
          </div>

          <div class="field">
            <label>character</label>
            <div class="control">
              <input type="text" class="input" v-model="character">
            </div>
          </div>

          <div class="field">
            <label>summary</label>
            <div class="control">
              <input type="text" class="input" v-model="summary">
            </div>
          </div>

          <div class="field">
            <label>Content</label>
            <div class="control">
              <textarea type="text" class="input" v-model="content" ></textarea>
            </div>
          </div>

          <div class="field">
            <div class="control">
              <button class="button is-success">Submit</button>
            </div>
          </div>

        </form>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    name: 'AddMbti',
    data() {
      return {
        board: '',
        mbti: '',
        image: '',
        title: '',
        content: '',
        character: '',
        summary: '',
      }
    },
    methods: {
      async submitForm() {
        this.$store.commit('setIsLoading', true)

        const mbti_ = {
          board: this.board,
          mbti: this.mbti,
          title: this.title,
          content: this.content,
          character: this.character,
          summary: this.summary,
          image: this.image
        }

        const headers = {
          'content-Type': 'multipart/form-data'
        }
        
        await axios
          .post('/mbti/', mbti_, {headers})
          .then(response => {
            console.log(response)
            this.$router.push('/dashboard/mbti')
          })

          .catch(error => {
            console.log(error)
          })
        this.$store.commit('setIsLoading', false)
      },

      async mbtiImage() {
        this.image = this.$refs.mbtiimage.files[0]
        console.log(this.image)
        return this.image
      }
    }
  }
</script>

<style>
  .field .control textarea {
    height: 300px;
  }
</style>