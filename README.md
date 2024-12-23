<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>VAST Ad Example</title>
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
    // Define the VAST ad URL
    const adTagUrl = "https://pubads.g.doubleclick.net/gampad/ads?iu=/22894150773/AdUnit-Test4-Video-WithoutCompanion&description_url=https%3A%2F%2Fadityasabnis.github.io%2Fget-talking%2F&tfcd=0&npa=0&ad_type=audio_video&sz=1x1%7C400x300%7C640x480&gdfp_req=1&unviewed_position_start=1&output=vast&env=vp&impl=s&correlator=";

    const videoContainer = document.getElementById('video-container');
    const contentVideo = document.getElementById('content-video');
    const adContainer = document.getElementById('ad-container');

    // Set up the Google IMA SDK
    const adDisplayContainer = new google.ima.AdDisplayContainer(adContainer, contentVideo);
    const adsLoader = new google.ima.AdsLoader(adDisplayContainer);
    const adsManagerSettings = new google.ima.AdsRenderingSettings();
    const adsRequest = new google.ima.AdsRequest();

    // Configure the ad request
    adsRequest.adTagUrl = adTagUrl;
    adsRequest.linearAdSlotWidth = videoContainer.offsetWidth;
    adsRequest.linearAdSlotHeight = videoContainer.offsetHeight;
    adsRequest.nonLinearAdSlotWidth = videoContainer.offsetWidth;
    adsRequest.nonLinearAdSlotHeight = videoContainer.offsetHeight / 3;

    // Initialize the IMA SDK when user interacts with the page
    videoContainer.addEventListener('click', () => {
      adDisplayContainer.initialize();
      contentVideo.load();

      // Request ads
      adsLoader.requestAds(adsRequest);

      // Set up content playback
      adsLoader.addEventListener(
        google.ima.AdsManagerLoadedEvent.Type.ADS_MANAGER_LOADED,
        (adsManagerLoadedEvent) => {
          const adsManager = adsManagerLoadedEvent.getAdsManager(contentVideo, adsManagerSettings);

          adsManager.addEventListener(
            google.ima.AdErrorEvent.Type.AD_ERROR,
            (adErrorEvent) => console.error(adErrorEvent.getError())
          );

          adsManager.addEventListener(
            google.ima.AdEvent.Type.ALL_ADS_COMPLETED,
            () => contentVideo.play()
          );

          // Start ad playback
          adsManager.init(videoContainer.offsetWidth, videoContainer.offsetHeight, google.ima.ViewMode.NORMAL);
          adsManager.start();
        }
      );

      adsLoader.addEventListener(
        google.ima.AdErrorEvent.Type.AD_ERROR,
        (adErrorEvent) => console.error(adErrorEvent.getError())
      );
    });
  </script>
</body>
</html>
