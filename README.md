# laavfoundationesstiosswift
##2. AVFoundation Fundamentals
###1 An overview of AVFoundation
####03:01
basic camera:
```
UIImagePickerController
```
####04:36
audio capture
```
AVRecorder
AVAudioPlayer
```
```
AVCaptureSession
```
Playback
```
AVPlayerLayer
```
Editing
```
AVComposition
```

###2 Concurrent programming with AVFoundation
####General guidelines
UI notifications on main thread.  
use ```NSThread,isMainThread```
to test


##2. Audio Recording
###1 Introduction to AVAudioRecorder
####01:31
```
AVCaptureAudioDataOutput
OpenAL
```
####01:44
before recording  
AV Audio Session singleton
```
AVAudioSession.sharedInstance
```
####02:45
```
AVAudioRecorder.settings
```
Recordomg options:
```
AVAudioRecorder.record()
```
####04:40AVAudioRecorderDelegate
```
audioRecorderDidFinishRecording
audioRecorderEncodeErrorDidOccur
```
