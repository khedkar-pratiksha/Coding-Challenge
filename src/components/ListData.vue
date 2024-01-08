<template>
<div>
    <div class="m-2">
      <h1 class="text-center text-primary">POSTS</h1>
      <table class="table table-bordered table-striped table-hover">
        <tr>
          <th>ID</th>
          <th>Title</th>
          <th>Body</th>
          <th>Reaction</th>
          <th>Tags</th>
          <th>User ID</th>
          <th>Action</th>
        </tr>
        <tr v-for="post in tableData" :key="post.id">
          <td>{{ post.id }}</td>
          <td>{{ post.title }}</td>
          <td>{{ post.body }}</td>
          <td>{{ post.reactions }}</td>
          <td>
            <ul>
              <li v-for="tag in post.tags" :key="tag">
                {{ tag }}
              </li>
            </ul>
          </td>
          <td>{{post.userId}}</td>
          <td>
            <button type="button" @click="getComments(post.id)" class="btn btn-info" data-bs-toggle="modal" data-bs-target="#staticBackdrop">Comments</button>
          </td>
        </tr>
      </table>
    </div>
    <div class="modal fade" id="staticBackdrop" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabel" aria-hidden="true">
      <div class="modal-dialog modal-dialog-scrollable .modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Comments</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <p v-if="comments.length===0">No comments.</p>
            <ul v-else>
              <li v-for="comment in comments" :key="comment.id">
                <strong> {{ comment.user.username }} </strong>
                <p>{{ comment.body }}</p>
              </li>
            </ul>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
          </div>
        </div>
      </div>
    </div>
</div>
</template>

<script>
export default {
  name: 'ListData',
  data () {
    return {
      tableData: [],
      isModalVisible: false,
      comments: []
    };
  },
  async mounted() {
    fetch('https://dummyjson.com/posts').then( (response) => {
      if (response.ok) {
        return response.json();
      }
    }).then( (data) => {
        this.tableData = data.posts;
    }).catch( (error) => {
      console.log(error);
    });
  },
  methods: {
    getComments (postId) {
      fetch(`https://dummyjson.com/posts/${postId}/comments `).then( (response) => {
        if (response.ok) {
          return response.json();
        }
      }).then( (data) => {
        if (data.total > 0) {
          this.comments = data.comments;
          this.isModalVisible = true;
        } else {
          this.comments = [];
          this.isModalVisible = false;
        }
      }).catch( (error) => {
        console.log(error);
      });
    }
  },
}
</script>

<style scoped>
</style>
