# js-memo

# Drag/Drop file

```

    $('#newpost')
      .on(
        'drag dragstart dragend dragover dragenter dragleave drop',
        (e: any) => {
          if (
            e.originalEvent.dataTransfer &&
            isDataTransferFile(e.originalEvent.dataTransfer.types)
          ) {
            e.preventDefault()
            e.stopPropagation()
          }
        }
      )
      .on('dragover', (e: any) => {
        if (
          e.originalEvent.dataTransfer &&
          isDataTransferFile(e.originalEvent.dataTransfer.types)
        ) {
          this.fileDragover()
        }
      })
      .on('dragenter', (e: any) => {
        if (
          e.originalEvent.dataTransfer &&
          isDataTransferFile(e.originalEvent.dataTransfer.types)
        ) {
          this.fileDragenter()
        }
      })
      .on('dragleave', (e: any) => {
        if (
          e.originalEvent.dataTransfer &&
          isDataTransferFile(e.originalEvent.dataTransfer.types)
        ) {
          this.fileDragleave()
        }
      })
      .on('drop', async (e: any) => {
        if (
          e.originalEvent.dataTransfer &&
          e.originalEvent.dataTransfer.files.length > 0
        ) {
          await this.onDragDropFileChange(e.originalEvent)
        }

        this.fileDrop()
      })
  }


const isDataTransferFile = (types: any) => {
    if(!types){
      return false
    }

    // For Chrome And IE
    if(types[0] === 'Files'){
      return true
    }

    // For Firefox
    if(types.includes && types.includes('Files')){
      return true
    }

    return false
}

  ```

# 