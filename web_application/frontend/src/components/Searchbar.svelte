<script>
  import { fetchAllCommentsFromVideo } from "../api";
  import { allVideoComments } from "../stores/CommentStore";

  let searchUrl = "";

  async function searchVideo(event) {
    const videoId = searchUrl.split("=")[1].split("&")[0];

    const {
      data: { videoComments, message },
      status,
    } = await fetchAllCommentsFromVideo(videoId);
    console.log(message)
    if (status == 200) {
      allVideoComments.set(videoComments);
    }
  }
</script>

<div class="main-search-area">
  <div class="search-area">
    <label for="search-bar" class="search-label"
      >Enter YouTube video link to get Comments</label
    >
    <input
      type="text"
      id="search-bar"
      class="search-bar"
      bind:value={searchUrl}
    />
  </div>
  <button on:click={searchVideo} class="search-submit">Go</button>
</div>

<style>
  .main-search-area {
    display: flex;
    align-items: stretch;
    justify-content: center;
    margin: 1rem 0 0 0;
  }

  .search-area {
    display: flex;
    align-items: stretch;
    flex-direction: column;
    justify-content: center;
  }

  /* .search-label{
  } */
  .search-bar,.search-submit {
    background-color: #c6e3eb;
  }
  /* .search-bar {
  }
  .search-submit {
  } */
</style>
