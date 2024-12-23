<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Video Ad Integration</title>
    <script src="https://imasdk.googleapis.com/js/sdkloader/ima3.js"></script>
    <style>
      #video-container {
        position: relative;
        width: 640px;
        height: 360px;
        background-color: black;
      }
      video {
        width: 100%;
        height: 100%;
      }
    </style>
  </head>
  <body>
    <div id="video-container">
      <video id="content-video" controls></video>
      <div id="ad-container"></div>
    </div>

    <script>
      // Your VAST tag URL
      const adTagUrl =
        "https://pubads.g.doubleclick.net/gampad/ads?iu=/22894150773/AdUnit-Test4-Video-WithoutCompanion&description_url=[placeholder]&tfcd=0&npa=0&ad_type=audio_video&sz=1x1%7C400x300%7C640x480&gdfp_req=1&unviewed_position_start=1&output=vast&env=vp&impl=s&correlator="; // Replace with your actual VAST tag URL

      const videoContainer = document.getElementById("video-container");
      const contentVideo = document.getElementById("content-video");
      const adContainer = document.getElementById("ad-container");

      // IMA SDK setup
      const adDisplayContainer = new google.ima.AdDisplayContainer(
        adContainer,
        contentVideo
      );
      const adsLoader = new google.ima.AdsLoader(adDisplayContainer);

      // Request ads when user interacts
      videoContainer.addEventListener("click", () => {
        adDisplayContainer.initialize();
        const adsRequest = new google.ima.AdsRequest();
        adsRequest.adTagUrl = adTagUrl;

        adsLoader.requestAds(adsRequest);

        adsLoader.addEventListener(
          google.ima.AdsManagerLoadedEvent.Type.ADS_MANAGER_LOADED,
          (adsManagerLoadedEvent) => {
            const adsManager =
              adsManagerLoadedEvent.getAdsManager(contentVideo);
            adsManager.init(640, 360, google.ima.ViewMode.NORMAL);
            adsManager.start();
          }
        );
      });
    </script>
  </body>
</html>
