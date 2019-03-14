```

  private async getGifData() {
    if (!this.isGif()) {
      return null
    }

    const readImageData = async (inputFile: File) => {
      const temporaryFileReader = new FileReader()

      return new Promise<GifData>((resolve: Function, reject: Function) => {
        temporaryFileReader.addEventListener('error', e => {
          reject(e)
        })

        temporaryFileReader.addEventListener('load', () => {
          // file is loaded
          const img = document.createElement('img')
          img.addEventListener('load', () => {
            resolve({
              gifFrames: 0,
              gifHeight: img.width,
              gifWidth: img.height,
            })
          })
          img.src = window.URL.createObjectURL(inputFile) // is the data URL because called with readAsDataURL
        })

        temporaryFileReader.readAsDataURL(inputFile)
      })
        .then(gifData => {
          return gifData
        })
        .catch(_e => {
          this.isCanValidateGifData = false
          return {
            gifFrames: 0,
            gifHeight: 0,
            gifWidth: 0,
          }
        })
    }

    try {
      return await readImageData(this.values.file)
    } catch (e) {
      throw e
    }
  }
}

```