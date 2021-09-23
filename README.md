# Golang Transcoding Library

## Features

<dl>
  <dt>Ease use</dt>
  <dd>Implement your own business logic around easy interfaces</dd>

  <dt>Transcoding progress</dt>
  <dd>Obtain progress events generated by transcoding application process</dd>
</dl>

## Download from Github

```shell
go get github.com/legion-zver/transcoder
```

## Example

```go
package main

import (
	"log"

	ffmpeg "github.com/legion-zver/transcoder/ffmpeg"
)

func main() {

	format := "mp4"
	overwrite := true

	opts := ffmpeg.Options{
		OutputFormat: &format,
		Overwrite:    &overwrite,
	}

	ffmpegConf := &ffmpeg.Config{
		FfmpegBinPath:   "/usr/local/bin/ffmpeg",
		FfprobeBinPath:  "/usr/local/bin/ffprobe",
		ProgressEnabled: true,
	}

	progress, err := ffmpeg.
		New(ffmpegConf).
		Input("/tmp/avi").
		Output("/tmp/mp4").
		WithOptions(opts).
		Start(opts)

	if err != nil {
		log.Fatal(err)
	}

	for msg := range progress {
		log.Printf("%+v", msg)
	}
}
```
