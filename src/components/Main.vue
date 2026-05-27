<script setup>
import { nextTick, onMounted, ref, watch } from 'vue'
import { RefreshRight } from '@element-plus/icons-vue'

const baseUrl = import.meta.env.BASE_URL || '/'
const publicAsset = (path) => `${baseUrl.replace(/\/?$/, '/')}${path.replace(/^\/+/, '')}`

const trajPlaybackRate = ref(1)
const trajPlaybackMarks = {
  0.5: '0.5x',
  1: '1x',
  1.5: '1.5x',
  2: '2x',
}

const trajectoryVideos = [
  {
    id: 'traj1',
    src: publicAsset('video/new_depthandmap/2_final.mp4'),
    label: 'Scenario 1',
  },
  {
    id: 'traj2',
    src: publicAsset('video/new_depthandmap/3_final.mp4'),
    label: 'Scenario 2',
  },
  {
    id: 'traj3',
    src: publicAsset('video/new_depthandmap/5_final.mp4'),
    label: 'Scenario 3',
  },
]

const comparisonVideos = [
  {
    id: 'allalg1',
    src: publicAsset('video/allalg/2050.mp4'),
    label: '20 Static & 50 Dynamic',
  },
  {
    id: 'allalg2',
    src: publicAsset('video/allalg/3060.mp4'),
    label: '30 Static & 60 Dynamic',
  },
  {
    id: 'allalg3',
    src: publicAsset('video/allalg/4070.mp4'),
    label: '40 Static & 70 Dynamic',
  },
]

const trackingVideos = [
  {
    id: 'catch1',
    src: publicAsset('video/catch/catch1.mp4'),
  },
  {
    id: 'catch2',
    src: publicAsset('video/catch/catch4.mp4'),
  },
  {
    id: 'catch3',
    src: publicAsset('video/catch/catch3.mp4'),
  },
  {
    id: 'catch4',
    src: publicAsset('video/catch/catch2.mp4'),
  },
]

const realWorldStaticVideos = [
  {
    id: 'realworldstatic1',
    src: publicAsset('video/static/static1.mp4'),
    label: 'Static flight 1',
  },
  {
    id: 'realworldstatic2',
    src: publicAsset('video/static/static2.mp4'),
    label: 'Static flight 2',
  },
]

const realWorldDynamicVideos = [
  {
    id: 'realworlddynamic1',
    src: publicAsset('video/final1.mp4'),
    label: 'Dynamic flight 1',
  },
  {
    id: 'realworlddynamic2',
    src: publicAsset('video/final2.mp4'),
    label: 'Dynamic flight 2',
  },
]

function setTrajVideoPlaybackRate() {
  const trajVideos = document.querySelectorAll("video[data-key^='traj']")
  trajVideos.forEach((video) => {
    video.playbackRate = trajPlaybackRate.value
  })
}

function formatTrajPlaybackTooltip(value) {
  return `${value}x`
}

function restartVideos(selector, playbackRate) {
  const videos = document.querySelectorAll(selector)
  videos.forEach((video) => {
    video.currentTime = 0

    if (playbackRate) {
      video.playbackRate = playbackRate
    }

    const playPromise = video.play()
    if (playPromise && typeof playPromise.catch === 'function') {
      playPromise.catch(() => {})
    }
  })
}

watch(trajPlaybackRate, () => {
  nextTick(setTrajVideoPlaybackRate)
})

onMounted(() => {
  setTrajVideoPlaybackRate()
})

function restarttrajVideos() {
  restartVideos("video[data-key^='traj']", trajPlaybackRate.value)
}

function restartAllAlgVideos() {
  restartVideos("video[data-key^='allalg']")
}

function restartCatchVideos() {
  restartVideos("video[data-key^='catch']")
}

function restartRealWorldStaticVideos() {
  restartVideos("video[data-key^='realworldstatic']")
}

function restartRealWorldDynamicVideos() {
  restartVideos("video[data-key^='realworlddynamic']")
}
</script>

<template>
  <main class="project-page">
    <section class="hero-section">
      <div class="content-shell content-shell--hero">
        <h1 class="project-title">
          <span class="project-title-brand">AeroDiffusion:</span>
          Real-Time Quadrotor Trajectory Planning in Dynamic Environments via Conditional Diffusion
        </h1>

        <figure class="hero-figure">
          <img
            :src="publicAsset('total.png')"
            alt="AeroDiffusion overview"
            class="hero-image"
          >
        </figure>

        <p class="abstract-copy">
          Safe and efficient navigation in dynamic environments remains a major challenge for quadrotors. In this paper, we propose AeroDiffusion, a conditional diffusion-based end-to-end trajectory planning framework for real-time quadrotor navigation in dynamic environments. By conditioning a diffusion model on depth images and vehicle states, AeroDiffusion generates dynamically feasible trajectories through an iterative denoising process. AeroDiffusion explicitly exploits the multi-modality of diffusion models by sampling a batch of candidate trajectories at each replanning step. These candidates are evaluated and selected using a preference-guided cost, enabling flexible behavior modulation without retraining. To further support real-time deployment, we introduce a warm-start replanning strategy that initializes diffusion from a partially noised previous trajectory, significantly reducing inference latency while preserving temporal consistency. Extensive experiments demonstrate that AeroDiffusion achieves superior safety, efficiency, robustness, and generalization.
        </p>
      </div>
    </section>

    <section class="paper-section">
      <div class="content-shell content-shell--wide">
        <div class="section-heading">
          <p class="section-kicker">Simulation</p>
          <h2>Dynamic Obstacle Navigation</h2>
        </div>

        <p class="section-copy">
          This section presents three representative flight demonstrations in environments populated with both static and dynamic obstacles. Each video shows the quadrotor's current onboard depth observation together with the map visualization and the multimodal candidate trajectories planned by the quadrotor. Pink obstacles represent dynamic obstacles, and the jet-colored obstacles represent static obstacles.
        </p>

        <div class="video-grid video-grid--three video-grid--trajectory">
          <figure
            v-for="video in trajectoryVideos"
            :key="video.id"
            class="media-card media-card--trajectory"
          >
            <div class="media-frame media-frame--trajectory">
              <video
                :data-key="video.id"
                autoplay
                loop
                muted
                preload="auto"
                playsinline
                class="media-video"
                controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
              >
                <source :src="video.src" type="video/mp4">
              </video>
            </div>
            <figcaption>{{ video.label }}</figcaption>
          </figure>
        </div>

        <div class="control-panel control-panel--speed">
          <span class="speed-label">Playback Speed: {{ trajPlaybackRate }}x</span>
          <div class="speed-slider">
            <el-slider
              v-model="trajPlaybackRate"
              :min="0.5"
              :max="2"
              :step="0.1"
              :marks="trajPlaybackMarks"
              :format-tooltip="formatTrajPlaybackTooltip"
            />
          </div>
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restarttrajVideos"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section class="paper-section paper-section--alt">
      <div class="content-shell">
        <div class="section-heading">
          <p class="section-kicker">Benchmark</p>
          <h2>Algorithm Comparison</h2>
        </div>

        <p class="section-copy">
          This section compares the proposed method against several state-of-the-art UAV obstacle avoidance algorithms under varying obstacle densities. Three scenarios with increasing numbers of obstacles are evaluated to assess scalability and robustness. In all settings, the maximum velocity of dynamic obstacles is set to 1.5 m/s.
        </p>

        <div class="video-grid video-grid--three">
          <figure
            v-for="video in comparisonVideos"
            :key="video.id"
            class="media-card"
          >
            <div class="media-frame media-frame--square">
              <video
                :data-key="video.id"
                autoplay
                loop
                muted
                preload="auto"
                playsinline
                class="media-video"
                controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
              >
                <source :src="video.src" type="video/mp4">
              </video>
            </div>
            <figcaption>{{ video.label }}</figcaption>
          </figure>
        </div>

        <div class="control-panel">
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartAllAlgVideos"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section class="paper-section">
      <div class="content-shell content-shell--wide">
        <div class="section-heading">
          <p class="section-kicker">Extension</p>
          <h2>Target Tracking Extension</h2>
        </div>

        <p class="section-copy">
          This section demonstrates an extension of the proposed planner to a target-tracking scenario involving two quadrotors. Both vehicles run the same algorithm, while the target of the trailing quadrotor is continuously set to the current position of the leading one. Without retraining, the planner naturally adapts to this formulation and generates smooth, collision-free trajectories that balance target following and obstacle avoidance.
        </p>

        <div class="video-grid video-grid--four video-grid--tracking">
          <figure
            v-for="video in trackingVideos"
            :key="video.id"
            class="media-card media-card--tracking"
          >
            <div class="media-frame media-frame--vertical">
              <video
                :data-key="video.id"
                autoplay
                loop
                muted
                preload="auto"
                playsinline
                class="media-video"
                controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
              >
                <source :src="video.src" type="video/mp4">
              </video>
            </div>
          </figure>
        </div>

        <div class="control-panel">
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartCatchVideos"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section class="paper-section paper-section--alt">
      <div class="content-shell">
        <div class="section-heading">
          <p class="section-kicker">Real World</p>
          <h2>Real-World Static Obstacles</h2>
        </div>

        <p class="section-copy">
          This section shows two real-world flight demonstrations in static obstacle environments. The top view illustrates the global trajectory of the quadrotor, while the bottom-left and bottom-right views correspond to onboard RGB observations and odometry-based mapping visualization, respectively. The map is pre-built by a separate UAV equipped with a Mid-360 LiDAR and is used only for visualization, not for planning. The quadrotor is commanded to fly to a waypoint located 8 m straight ahead and then return to the origin.
        </p>

        <div class="video-grid video-grid--two">
          <figure
            v-for="video in realWorldStaticVideos"
            :key="video.id"
            class="media-card"
          >
            <div class="media-frame media-frame--square">
              <video
                :data-key="video.id"
                autoplay
                loop
                muted
                preload="auto"
                playsinline
                class="media-video"
                controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
              >
                <source :src="video.src" type="video/mp4">
              </video>
            </div>
            <figcaption>{{ video.label }}</figcaption>
          </figure>
        </div>

        <div class="control-panel">
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartRealWorldStaticVideos"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section class="paper-section">
      <div class="content-shell">
        <div class="section-heading">
          <p class="section-kicker">Real World</p>
          <h2>Real-World Dynamic Obstacles</h2>
        </div>

        <p class="section-copy">
          This section presents two real-world demonstrations involving dynamic obstacles. The top view shows the global flight trajectory, while the bottom views display onboard depth and RGB camera observations.
        </p>

        <div class="video-grid video-grid--two">
          <figure
            v-for="video in realWorldDynamicVideos"
            :key="video.id"
            class="media-card"
          >
            <div class="media-frame media-frame--square">
              <video
                :data-key="video.id"
                autoplay
                loop
                muted
                preload="auto"
                playsinline
                class="media-video"
                controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
              >
                <source :src="video.src" type="video/mp4">
              </video>
            </div>
            <figcaption>{{ video.label }}</figcaption>
          </figure>
        </div>

        <div class="control-panel">
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartRealWorldDynamicVideos"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.project-page {
  --page-ink: #17201f;
  --muted-ink: #586462;
  --paper: #fbfbf8;
  --panel: #ffffff;
  --panel-soft: #f2f6f4;
  --line: #dbe4e0;
  --accent: #1f7a70;
  --accent-dark: #14544e;
  --warm: #b57d2c;

  min-height: 100vh;
  color: var(--page-ink);
  background: var(--paper);
}

.content-shell {
  width: min(1080px, calc(100% - 40px));
  margin: 0 auto;
}

.content-shell--hero {
  width: min(1160px, calc(100% - 40px));
}

.content-shell--wide {
  width: min(1220px, calc(100% - 40px));
}

.hero-section {
  padding: 54px 0 58px;
  background: #eef4f1;
  border-bottom: 1px solid var(--line);
}

.section-kicker {
  margin: 0 0 10px;
  color: var(--accent-dark);
  font-family: "DemiFont", "Arial", sans-serif;
  font-size: 16px;
  line-height: 1.35;
  text-align: center;
}

.project-title {
  max-width: 1040px;
  margin: 0 auto;
  color: #111a19;
  font-family: "BoldFont", Times, "Times New Roman", serif;
  font-size: 42px;
  line-height: 1.16;
  letter-spacing: 0;
  text-align: center;
}

.project-title-brand {
  color: var(--accent-dark);
}

.hero-figure {
  max-width: 980px;
  margin: 34px auto 0;
  overflow: hidden;
  border: 1px solid #cddbd6;
  border-radius: 8px;
  background: var(--panel);
  box-shadow: 0 18px 42px rgba(24, 45, 42, 0.12);
}

.hero-image {
  display: block;
  width: 100%;
  height: auto;
}

.abstract-copy {
  max-width: 980px;
  margin: 28px auto 0;
  padding-left: 20px;
  border-left: 4px solid var(--warm);
  color: #283331;
  font-size: 19px;
  line-height: 1.72;
  text-align: justify;
}

.paper-section {
  padding: 58px 0 62px;
  border-bottom: 1px solid var(--line);
  background: var(--paper);
}

.paper-section--alt {
  background: var(--panel-soft);
}

.section-heading {
  max-width: 900px;
  margin: 0 auto 24px;
}

.section-heading h2 {
  color: #14201e;
  font-family: "BoldFont", Times, "Times New Roman", serif;
  font-size: 30px;
  line-height: 1.22;
  letter-spacing: 0;
  text-align: center;
}

.section-copy {
  max-width: 1000px;
  margin: 0 auto 28px;
  color: #2c3735;
  font-size: 18px;
  line-height: 1.72;
  text-align: justify;
}

.video-grid {
  display: grid;
  gap: 22px;
  align-items: start;
}

.video-grid--two {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.video-grid--three {
  grid-template-columns: repeat(3, minmax(0, 1fr));
}

.video-grid--four {
  grid-template-columns: repeat(4, minmax(0, 1fr));
}

.video-grid--trajectory {
  max-width: 1060px;
  margin: 0 auto;
}

.video-grid--tracking {
  max-width: 1040px;
  margin: 0 auto;
}

.media-card {
  margin: 0;
  padding: 10px;
  overflow: hidden;
  border: 1px solid var(--line);
  border-radius: 8px;
  background: var(--panel);
  box-shadow: 0 10px 26px rgba(24, 45, 42, 0.08);
}

.media-card--trajectory {
  max-width: 340px;
  justify-self: center;
  width: 100%;
}

.media-card--tracking {
  max-width: 260px;
  justify-self: center;
  width: 100%;
}

.media-frame {
  overflow: hidden;
  border-radius: 6px;
  background: #0f1717;
}

.media-frame--square {
  aspect-ratio: 1 / 1;
}

.media-frame--trajectory {
  aspect-ratio: 10 / 23;
}

.media-frame--vertical {
  aspect-ratio: 9 / 16;
}

.media-video {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

figcaption {
  min-height: 22px;
  margin-top: 10px;
  color: var(--muted-ink);
  font-family: "DemiFont", "Arial", sans-serif;
  font-size: 15px;
  line-height: 1.45;
  text-align: center;
}

.control-panel {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 18px;
  width: fit-content;
  max-width: 100%;
  margin: 26px auto 0;
  padding: 12px 16px;
  border: 1px solid var(--line);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.86);
  box-shadow: 0 8px 22px rgba(24, 45, 42, 0.07);
}

.control-panel--speed {
  width: min(760px, 100%);
  flex-wrap: wrap;
}

.speed-label {
  flex: 0 0 auto;
  min-width: 180px;
  color: #26312f;
  font-family: "DemiFont", "Arial", sans-serif;
  font-size: 16px;
  line-height: 1.4;
  text-align: right;
  white-space: nowrap;
}

.speed-slider {
  flex: 1 1 310px;
  max-width: 360px;
  min-width: 240px;
  padding: 0 8px;
}

.project-page :deep(.el-slider__runway) {
  background-color: #d9e5e1;
}

.project-page :deep(.el-slider__bar) {
  background-color: var(--accent);
}

.project-page :deep(.el-slider__button) {
  border-color: var(--accent);
}

.project-page :deep(.el-slider__marks-text) {
  color: var(--muted-ink);
  font-family: "DemiFont", "Arial", sans-serif;
  font-size: 12px;
}

.project-page :deep(.el-button.custom-button) {
  min-height: 40px;
  border: 0;
  border-radius: 6px;
  background: var(--accent);
  font-family: "DemiFont", "Arial", sans-serif;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0;
}

.project-page :deep(.el-button.custom-button:hover),
.project-page :deep(.el-button.custom-button:focus) {
  background: var(--accent-dark);
}

@media (max-width: 980px) {
  .video-grid--four,
  .video-grid--three {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }

  .project-title {
    font-size: 36px;
  }
}

@media (max-width: 720px) {
  .content-shell,
  .content-shell--hero,
  .content-shell--wide {
    width: min(100% - 28px, 640px);
  }

  .hero-section {
    padding: 38px 0 44px;
  }

  .paper-section {
    padding: 44px 0 48px;
  }

  .project-title {
    font-size: 30px;
    line-height: 1.2;
  }

  .section-heading h2 {
    font-size: 26px;
  }

  .abstract-copy,
  .section-copy {
    font-size: 17px;
    line-height: 1.66;
    text-align: left;
  }

  .abstract-copy {
    padding-left: 16px;
  }

  .video-grid,
  .video-grid--two,
  .video-grid--three,
  .video-grid--four {
    grid-template-columns: 1fr;
  }

  .video-grid--tracking {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 14px;
  }

  .media-card {
    padding: 8px;
  }

  .control-panel {
    width: 100%;
  }

  .control-panel--speed {
    align-items: stretch;
  }

  .speed-label {
    min-width: 0;
    text-align: center;
  }

  .speed-slider {
    max-width: none;
    min-width: 0;
    width: 100%;
  }
}

@media (max-width: 420px) {
  .project-title {
    font-size: 27px;
  }

  .video-grid--tracking {
    grid-template-columns: 1fr;
  }
}
</style>
