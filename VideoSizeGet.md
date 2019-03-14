```

  private async getVideoData() {
    if (!this.isVideo()) {
      return null
    }

    const readVideoDuration = async (inputFile: File) => {
      return new Promise<VideoData>((resolve: Function, reject: Function) => {
        const url = window.URL.createObjectURL(inputFile)
        const video = document.createElement('video')
        video.src = url
        video.addEventListener('durationchange', () => {
          resolve({
            duration: video.duration,
            videoHeight: video.videoHeight,
            videoWidth: video.videoWidth,
          })
        })
        video.addEventListener('error', e => {
          reject(e)
        })
      })
        .then(videoData => {
          return videoData
        })
        .catch(_e => {
          this.isCanValidateVideoData = false
          return {
            duration: 0,
            videoHeight: MIN_VIDEO_HEIGHT,
            videoWidth: MIN_VIDEO_WIDTH,
          }
        })
    }
    try {
      return await readVideoDuration(this.values.file)
    } catch (e) {
      throw e
    }
  }

```