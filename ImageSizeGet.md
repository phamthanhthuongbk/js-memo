```

  private async getImageData(file) {
    if (!this.isImage()) {
      return null
    }

    const readImageData = async (inputFile: File) => {
      const temporaryFileReader = new FileReader()

      return new Promise<ImageData>((resolve: Function, reject: Function) => {
        temporaryFileReader.addEventListener('error', e => {
          reject(e)
        })

        temporaryFileReader.addEventListener('load', () => {
          // file is loaded
          const img = document.createElement('img')
          img.addEventListener('load', () => {
            resolve({
              imageHeight: img.width,
              imageWidth: img.height,
            })
          })
          img.src = window.URL.createObjectURL(inputFile) // is the data URL because called with readAsDataURL
        })

        temporaryFileReader.readAsDataURL(inputFile)
      })
        .then(imageData => {
          return imageData
        })
        .catch(_e => {
          this.isCanValidateImageData = false
          return {
            imageHeight: 0,
            imageWidth: 0,
          }
        })
    }

    try {
      return await readImageData(file)
    } catch (e) {
      throw e
    }
  }

```
