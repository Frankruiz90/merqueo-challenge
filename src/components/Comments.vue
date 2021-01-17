<template>
  <div class="container-card">
    <div class="container-input">
      <input
        type="text"
        class="container-input__text"
        placeholder="Escribe aquí tu nombre"
        v-model="name"
        @keyup.enter="seeStates = !seeStates"
      />
    </div>
    <div v-if="seeStates">
      <div class="container-input">
        <input
          type="text"
          class="container-input__text"
          placeholder="Escribe aquí tu estado"
          v-model="newComment"
          @keyup.enter="addComment()"
        />
        <div class="container-input-btn">
          <div class="btn-principal" @click="addComment()">Publicar</div>
        </div>
      </div>
      <div
        v-for="(comment, index) in comments"
        :key="index"
        class="card-principal"
      >
        <div class="card-icon">
          <img src="../assets/img/user.jpg" alt="" class="card-icon__icon" />
        </div>
        <div class="card-information">
          <h2 class="card-information__name">{{ comment.name }}</h2>
          <span class="card-information__time-comment">{{
            comment.timeComment
          }}</span>
          <h2 class="card-information__text-comment">
            {{ comment.myComment }}
          </h2>
          <div class="container-buttons">
            <div class="btn-secondary">Reaccionar</div>
            <div class="btn-secondary" @click="changeSeeComments(index)">
              Comentar
            </div>
          </div>
        </div>
        <div class="container-state">
          <div class="container-state__reactions">
            <div
              v-for="(state, index2) in comment.reactions"
              :key="index2"
              class="container-state__reactions-reactions btn-state"
              :class="{
                'btn-state__like': state.nameState === 'like',
                'btn-state__dont-like': state.nameState === 'dontLike',
                'btn-state__medium-like': state.nameState === 'mediumLike',
              }"
              @click="addMoreReactions(state.quantity, index, index2)"
            >
              <span>{{ state.quantity }}</span>
            </div>
          </div>
          <div class="container-state__comments">
            <span>{{ comment.comments.length }} Comentarios</span>
          </div>
        </div>
        <div class="container-buttons-small">
          <div class="btn-secondary">Reaccionar</div>
          <div class="btn-secondary" @click="changeSeeComments(index)">
            Comentar
          </div>
        </div>
        <div class="container-comments" v-if="seeComents[index]">
          <div
            v-for="(comments, index3) in comment.comments"
            :key="index3"
            class="container-comments__comment"
          >
            <div class="container-comments__comment-icon">
              <img
                src="../assets/img/user.jpg"
                alt=""
                class="container-comments__comment-icon__profile"
              />
            </div>
            <div class="container-comments__comment-name">
              {{ comments.nameComment }}
            </div>
            <div class="container-comments__comment-your-coment">
              {{ comments.yourComment }}
            </div>
            <div class="container-comments__comment-date">
              {{ comments.dateComment }}
            </div>
            <!-- <span>{{ comments }}</span> -->
          </div>
          <div class="container-input container-input-comment">
            <input
              type="text"
              class="container-input__text container-input-comment__comment"
              placeholder="Escribe un comentario"
              v-model="newCommentMyState"
              @keyup.enter="addNewComment(index)"
            />
          </div>
        </div>
        <!-- <label>{{ comments }}</label> -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      comments: [
        {
          name: "visit 1",
          timeComment: "hace 2 días",
          myComment: "hola este es mi comentario",
          reactions: [
            {
              nameState: "like",
              quantity: 3,
            },
            {
              nameState: "dontLike",

              quantity: 2,
            },
            {
              nameState: "mediumLike",

              quantity: 9,
            },
          ],
          comments: [
            {
              nameComment: "elina",
              yourComment: " hola mundo",
              dateComment: "Hace 3 días",
            },
            {
              nameComment: "hector",
              yourComment: " hola mundo2",
              dateComment: "Hace 3 días",
            },
          ],
        },
        {
          name: "visit 2",
          timeComment: "hace 2 días",
          myComment: "hola este es mi comentario 2",
          reactions: [
            {
              nameState: "like",
              quantity: 5,
            },
            {
              nameState: "dontLike",

              quantity: 5,
            },
            {
              nameState: "mediumLike",

              quantity: 4,
            },
          ],
          comments: [
            {
              nameComment: "elina",
              yourComment: " hola mundo",
              dateComment: "Hace 3 días",
            },
            {
              nameComment: "hector",
              yourComment: " hola mundo2",
              dateComment: "Hace 3 días",
            },
          ],
        },
        {
          name: "visit 3",
          timeComment: "hace 2 días",
          myComment: "hola este es mi comentario",
          reactions: [
            {
              nameState: "like",
              quantity: 3,
            },
            {
              nameState: "dontLike",

              quantity: 2,
            },
            {
              nameState: "mediumLike",

              quantity: 9,
            },
          ],
          comments: [],
        },
      ],
      seeComents: [],
      stateComment: false,
      seeReaction: false,
      newComment: "",
      newCommentMyState: "",
      countReactions: 0,
      name: "",
      seeStates: false,
    };
  },
  components: {},
  methods: {
    changeSeeComments(i) {
      this.seeComents[i] =
        this.seeComents[i] === true ? false : !this.stateComment;
    },
    addComment() {
      try {
        let newData = {
          name: this.name,
          timeComment: "hoy",
          myComment: this.newComment,
          reactions: [
            {
              nameState: "like",
              quantity: 0,
            },
            {
              nameState: "dontLike",

              quantity: 0,
            },
            {
              nameState: "mediumLike",

              quantity: 0,
            },
          ],
          comments: [],
        };
        this.comments.unshift(newData);
      } finally {
        this.newComment = "";
      }
    },
    addNewComment(i) {
      try {
        let newComment = {
          nameComment: this.name,
          yourComment: this.newCommentMyState,
          dateComment: "Hoy",
        };
        this.comments[i].comments.unshift(newComment);
      } finally {
        this.newCommentMyState = "";
      }
    },
    addMoreReactions(state, i, i2) {
      this.comments[i].reactions[i2].quantity = state + 1;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/sass/main";
</style>