<template>
  <div class="middle-pane">
    <div class="progress" id="progressPane">
      <h3 class="title">{{ song.title }}</h3>
      <p class="meta">
        <a class="artist" :href="`#!/artist/${song.artist.id}`">{{ song.artist.name }}</a> –
        <a class="album" :href="`#!/album/${song.album.id}`">{{ song.album.name }}</a>
      </p>

      <div class="plyr">
        <audio crossorigin="anonymous" controls></audio>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    song: {
      required: true,
      type: Object
    }
  }
}
</script>

<style lang="scss">/* no scoping here because we're overriding some plyr classes */
@import "~#/partials/_vars.scss";
@import "~#/partials/_mixins.scss";

$colorPaneBgr: darken($color2ndBgr, 3);

.middle-pane {
  flex: 1;
  display: flex;
  background: $colorPaneBgr;

  @media only screen and (max-width: 768px) {
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    height: 8px;
  }
}

#progressPane {
  flex: 1;
  position: relative;
  display: flex;
  flex-direction: column;
  place-content: center;
  place-items: center;

  .meta {
    font-size: .9rem;

    a {
      &:hover {
        color: $colorHighlight;
      }
    }
  }

  // Some little tweaks here and there
  .plyr {
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }

  .plyr__progress {
    &--seek {
      height: 11px;
      border-bottom: 10px solid $colorPaneBgr; // increase click area
    }
  }

  .plyr__controls {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    padding: 0;

    &--left, &--right {
      display: none;
    }
  }

  @media only screen and (max-width: 768px) {
    .meta, .title {
      display: none;
    }

    .plyr__progress {
      &--seek {
        border-bottom-color: $color2ndBgr;
      }
    }
  }
}
</style>
