<script setup>

import { nextTick, onMounted, ref, watch } from 'vue'

const trajPlaybackRate = ref(1)
const trajPlaybackMarks = {
  0.5: '0.5x',
  1: '1x',
  1.5: '1.5x',
  2: '2x',
}

function setTrajVideoPlaybackRate() {
  const trajVideos = document.querySelectorAll("video[data-key*='traj']");
  trajVideos.forEach(video => {
    video.playbackRate = trajPlaybackRate.value;
  });
}

function formatTrajPlaybackTooltip(value) {
  return `${value}x`;
}

watch(trajPlaybackRate, () => {
  nextTick(setTrajVideoPlaybackRate);
});

onMounted(() => {
  setTrajVideoPlaybackRate();
});

function restarttrajVideos() {
  const trajVideos = document.querySelectorAll("video[data-key*='traj']");
  trajVideos.forEach(video => {
    video.currentTime = 0;
    video.playbackRate = trajPlaybackRate.value;
    video.play();
  });
}

function restartAllAlgVideos() {
  const allAlgVideos = document.querySelectorAll("video[data-key*='allalg']");
  allAlgVideos.forEach(video => {
    video.currentTime = 0;
    video.play();
  });
}

function restartCatchVideos() {
  const allAlgVideos = document.querySelectorAll("video[data-key*='catch']");
  allAlgVideos.forEach(video => {
    video.currentTime = 0;
    video.play();
  });
}


function restartRealWorldStaticVideos() {
  const finalVideos = document.querySelectorAll("video[data-key*='realworldstatic']");
  finalVideos.forEach(video => {
    video.currentTime = 0;
    video.play();
  });
}

function restartRealWorldDynamicVideos() {
  const finalVideos = document.querySelectorAll("video[data-key*='realworlddynamic']");
  finalVideos.forEach(video => {
    video.currentTime = 0;
    video.play();
  });
}

function setVideosToStopAtLastFrame() {
  const videos = document.querySelectorAll("video");
  videos.forEach(video => {
    video.addEventListener("ended", () => {
      video.currentTime = video.duration - 0.01; // Set to the last frame
    });
  });
}


</script>


<template>
  <div style="height: 48px;"></div>
    <el-row justify="center" style="margin-bottom: 36px;">
      <el-col :xs="24" :sm="22" :md="22" :lg="20" :xl="16">
        <h1 class="section-title" style="margin-bottom: 28px;">AeroDiffusion: Real-Time Quadrotor Trajectory Planning in Dynamic Environments via Conditional Diffusion</h1>
      </el-col>
    </el-row>

  <div>
    <!-- <el-divider /> -->
    <el-row justify="center" style="margin-bottom: 36px;">
        <el-col :xs="24" :sm="20" :md="20" :lg="17" :xl="10">
            <!-- <h1 style="margin-bottom: 20px;">摘要</h1> -->
            <img src="/public/total.png" alt="Logo" style="width:100%;margin-bottom:12px;border-radius:10px;" />
            <p style="margin-bottom: 16px;">
Safe and efficient navigation in dynamic environments remains a major challenge for quadrotors. In this paper, we propose AeroDiffusion, a conditional diffusion–based end-to-end trajectory planning framework for real-time quadrotor navigation in dynamic environments. By conditioning a diffusion model on depth images and vehicle states, AeroDiffusion generates dynamically feasible trajectories through an iterative denoising process. AeroDiffusion explicitly exploits the multi-modality of diffusion models by sampling a batch of candidate trajectories at each replanning step. These candidates are evaluated and selected using a preference-guided cost, enabling flexible behavior modulation without retraining. To further support real-time deployment, we introduce a warm-start replanning strategy that initializes diffusion from a partially noised previous trajectory, significantly reducing inference latency while preserving temporal consistency. Extensive experiments demonstrate that AeroDiffusion achieves superior safety, efficiency, robustness, and generalization.
            </p>
        </el-col>
    </el-row>
  </div>


  <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 32px;">Dynamic Obstacle Navigation</h2>
    </el-row>
    <el-row justify="center" style="margin-bottom: 56px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="14">
        <p style="margin-bottom: 24px;">
This section presents three representative flight demonstrations in environments populated with both static and dynamic obstacles. In each row, the left video shows the quadrotor's current onboard depth observation, while the right video visualizes the map together with the multimodal candidate trajectories planned by the quadrotor. Pink obstacles represent dynamic obstacles, and the jet-colored obstacles represent static obstacles.
            </p>
        <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                <video key='traj1' data-key='traj1' autoplay loop muted preload playsinline style="width:92%;max-width:720px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/new_depthandmap/massive2_depth.mp4" type="video/mp4">
              </video>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                 <video key='traj2' data-key='traj2' autoplay loop muted preload playsinline style="width:92%;max-width:720px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/new_depthandmap/massive2_map.mp4" type="video/mp4">
               </video>
            </el-col>
        </el-row>
        
        <!-- 空行两行 -->
        <br />
        <br />

           <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                <video key='traj3' data-key='traj3' autoplay loop muted preload playsinline style="width:92%;max-width:720px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/new_depthandmap/massive3_depth.mp4" type="video/mp4">
              </video>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                 <video key='traj4' data-key='traj4' autoplay loop muted preload playsinline style="width:92%;max-width:720px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/new_depthandmap/massive3_map.mp4" type="video/mp4">
               </video>
            </el-col>
        </el-row>     

        <br />
        <br />
        

           <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                <video key='traj5' data-key='traj5' autoplay loop muted preload playsinline style="width:92%;max-width:720px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/new_depthandmap/massive5_depth.mp4" type="video/mp4">
              </video>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                 <video key='traj6' data-key='traj6' autoplay loop muted preload playsinline style="width:92%;max-width:720px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/new_depthandmap/massive5_map.mp4" type="video/mp4">
               </video>
            </el-col>
        </el-row>     


        <div style="height: 18px;"></div>
        <el-row justify="center" style="margin-bottom: 18px;">
          <el-col :xs="22" :sm="20" :md="18" :lg="16" :xl="12">
            <div style="display:flex;align-items:center;justify-content:center;column-gap:56px;row-gap:18px;flex-wrap:wrap;">
              <span style="width:190px;font-family:'BoldFont','DemiFont','Arial',sans-serif;font-size:16px;white-space:nowrap;color:#333;text-align:right;">
                Playback Speed: {{ trajPlaybackRate }}x
              </span>
              <div style="width:360px;max-width:100%;">
                <el-slider
                  v-model="trajPlaybackRate"
                  :min="0.5"
                  :max="2"
                  :step="0.25"
                  :marks="trajPlaybackMarks"
                  :format-tooltip="formatTrajPlaybackTooltip"
                />
              </div>
              <el-button type="primary" @click="restarttrajVideos" class="custom-button">Restart Videos</el-button>
            </div>
          </el-col>
        </el-row>
        
      </el-col>
    </el-row>
  </div>


<div>
  <el-divider />


<div>
  <el-divider />

  <el-row justify="center">
    <h2 class="section-title" style="margin-bottom: 32px;">
      Algorithm Comparison
    </h2>
  </el-row>

  <el-row justify="center" style="margin-bottom: 56px;">
    <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="16">
      <p style="margin-bottom: 24px;">
This section compares the proposed method against several state-of-the-art UAV obstacle avoidance algorithms under varying obstacle densities. Three scenarios with increasing numbers of obstacles are evaluated to assess scalability and robustness. In all settings, the maximum velocity of dynamic obstacles is set to 1.5 m/s.
      </p>

      <!-- 三视频行 -->
      <el-row justify="center" gutter="10">
        <!-- 视频 1 -->
        <el-col
          :xs="24"
          :sm="12"
          :md="8"
          :lg="8"
          :xl="8"
          style="display:flex;flex-direction:column;align-items:center;"
        >
          <video
            key="allalg1"
            data-key="allalg1"
            autoplay
            loop
            muted
            preload
            playsinline
            style="width:100%;max-width:800px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;"
            controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
          >
            <source src="/video/allalg/2050.mp4" type="video/mp4" />
          </video>

          <div
            style="
              margin-top: 12px;
              font-size: 14px;
              color: #666;
              text-align: center;
              line-height: 1.5;
            "
          >
            20 Static & 50 Dynamic
          </div>
        </el-col>

        <!-- 视频 2 -->
        <el-col
          :xs="24"
          :sm="12"
          :md="8"
          :lg="8"
          :xl="8"
          style="display:flex;flex-direction:column;align-items:center;"
        >
          <video
            key="allalg2"
            data-key="allalg2"
            autoplay
            loop
            muted
            preload
            playsinline
            style="width:100%;max-width:800px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;"
            controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
          >
            <source src="/video/allalg/3060.mp4" type="video/mp4" />
          </video>

          <div
            style="
              margin-top: 12px;
              font-size: 14px;
              color: #666;
              text-align: center;
              line-height: 1.5;
            "
          >
             30 Static & 60 Dynamic
          </div>
        </el-col>

        <!-- 视频 3 -->
        <el-col
          :xs="24"
          :sm="12"
          :md="8"
          :lg="8"
          :xl="8"
          style="display:flex;flex-direction:column;align-items:center;"
        >
          <video
            key="allalg3"
            data-key="allalg3"
            autoplay
            loop
            muted
            preload
            playsinline
            style="width:100%;max-width:800px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;"
            controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
          >
            <source src="/video/allalg/4070.mp4" type="video/mp4" />
          </video>

          <div
            style="
              margin-top: 12px;
              font-size: 14px;
              color: #666;
              text-align: center;
              line-height: 1.5;
            "
          >
            40 Static & 70 Dynamic
          </div>
        </el-col>
      </el-row>

      <div style="height: 18px;"></div>

      <el-row justify="center">
        <el-button
          type="primary"
          @click="restartAllAlgVideos"
          class="custom-button"
        >
          Restart Videos
        </el-button>
      </el-row>
    </el-col>
  </el-row>
</div>





  <el-row justify="center">
    <h2 class="section-title" style="margin-bottom: 32px;">
      Target Tracking Extension
    </h2>
  </el-row>

  <el-row justify="center" style="margin-bottom: 56px;">
    <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="16">
      <p style="margin-bottom: 24px;">
        This section demonstrates an extension of the proposed planner to a target-tracking scenario involving two quadrotors. Both vehicles run the same algorithm, while the target of the trailing quadrotor is continuously set to the current position of the leading one. Without retraining, the planner naturally adapts to this formulation and generates smooth, collision-free trajectories that balance target following and obstacle avoidance.
      </p>

      <!-- 四视频行 -->
      <el-row justify="center" gutter="10">
        <!-- Video 1 -->
        <el-col
          :xs="24"
          :sm="12"
          :md="6"
          :lg="6"
          :xl="6"
          style="display:flex;align-items:center;justify-content:center;"
        >
          <video
            key="catch1"
            data-key="catch1"
            autoplay
            loop
            muted
            preload
            playsinline
            style="width:100%;aspect-ratio:9/16;border-radius:10px;object-fit:cover;"
            controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
          >
            <source src="/video/catch/catch1.mp4" type="video/mp4" />
          </video>
        </el-col>

        <!-- Video 2 -->
        <el-col
          :xs="24"
          :sm="12"
          :md="6"
          :lg="6"
          :xl="6"
          style="display:flex;align-items:center;justify-content:center;"
        >
          <video
            key="catch2"
            data-key="catch2"
            autoplay
            loop
            muted
            preload
            playsinline
            style="width:100%;aspect-ratio:9/16;border-radius:10px;object-fit:cover;"
            controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
          >
            <source src="/video/catch/catch4.mp4" type="video/mp4" />
          </video>
        </el-col>

        <!-- Video 3 -->
        <el-col
          :xs="24"
          :sm="12"
          :md="6"
          :lg="6"
          :xl="6"
          style="display:flex;align-items:center;justify-content:center;"
        >
          <video
            key="catch3"
            data-key="catch3"
            autoplay
            loop
            muted
            preload
            playsinline
            style="width:100%;aspect-ratio:9/16;border-radius:10px;object-fit:cover;"
            controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
          >
            <source src="/video/catch/catch3.mp4" type="video/mp4" />
          </video>
        </el-col>

        <!-- Video 4 -->
        <el-col
          :xs="24"
          :sm="12"
          :md="6"
          :lg="6"
          :xl="6"
          style="display:flex;align-items:center;justify-content:center;"
        >
          <video
            key="catch4"
            data-key="catch4"
            autoplay
            loop
            muted
            preload
            playsinline
            style="width:100%;aspect-ratio:9/16;border-radius:10px;object-fit:cover;"
            controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
          >
            <source src="/video/catch/catch2.mp4" type="video/mp4" />
          </video>
        </el-col>
      </el-row>

      <div style="height: 18px;"></div>

      <el-row justify="center">
        <el-button
          type="primary"
          @click="restartCatchVideos"
          class="custom-button"
        >
          Restart Videos
        </el-button>
      </el-row>
    </el-col>
  </el-row>
</div>



    <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 32px;">Real-World Static Obstacles</h2>
    </el-row>
    <el-row justify="center" style="margin-bottom: 56px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="14">
        <p style="margin-bottom: 24px;">
This section shows two real-world flight demonstrations in static obstacle environments. The top view illustrates the global trajectory of the quadrotor, while the bottom-left and bottom-right views correspond to onboard RGB observations and odometry-based mapping visualization, respectively. The map is pre-built by a separate UAV equipped with a Mid-360 LiDAR and is used only for visualization, not for planning. The quadrotor is commanded to fly to a waypoint located 8 m straight ahead and then return to the origin.
        </p>
        <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                <video key='realworldstatic1' data-key='realworldstatic1' autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/static/static1.mp4" type="video/mp4">
              </video>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                 <video key='realworldstatic2' data-key='realworldstatic2' autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/static/static2.mp4" type="video/mp4">
               </video>
            </el-col>
        </el-row>

        <div style="height: 18px;"></div>
        <el-row justify="center">
          <el-button type="primary" @click="restartRealWorldStaticVideos" class="custom-button">Restart Videos</el-button>
        </el-row>
        
      </el-col>
    </el-row>
  </div>

    <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 32px;">Real-World Dynamic Obstacles</h2>
    </el-row>
    <el-row justify="center" style="margin-bottom: 56px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="14">
        <p style="margin-bottom: 24px;">
This section presents two real-world demonstrations involving dynamic obstacles. The top view shows the global flight trajectory, while the bottom views display onboard depth and RGB camera observations.
        </p>
        <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                <video key='realworlddynamic1' data-key='realworlddynamic1' autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/final1.mp4" type="video/mp4">
              </video>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
                 <video key='realworlddynamic2' data-key='realworlddynamic2' autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/final2.mp4" type="video/mp4">
               </video>
            </el-col>
        </el-row>

        <div style="height: 18px;"></div>
        <el-row justify="center">
          <el-button type="primary" @click="restartRealWorldDynamicVideos" class="custom-button">Restart Videos</el-button>
        </el-row>
        
      </el-col>
    </el-row>
  </div>

</template>
