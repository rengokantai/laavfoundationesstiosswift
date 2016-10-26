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

###2 Record audio
AudioViewController.swift
```
import UIKit
import AVFoundation
class AudioViewController:UIViewVontroller{
  @IBOutlet weak var recordButton:UIButton!
  @IBOutlet weak var playButton:UIButton!
  var audioRecorder:AVAudioRecorder!
  @IBAction func recordButtonPressed(sender:AnyObject){}
  @IBAction func playButtonPressed(sender:AnyObject){}
  
  func audioFileLocation()->String{ return NATemporaryDirectory().appending("audio.m4a")}
  
  func audiorerderSettings()->[String:Any]{
    let settings = [AVFormatIDKey:NSNumber.init(value:kAudioFormatAppleLossless),AVSampleRateKey:NSNumber.init(value:44100.0),AVNumberOfChannelsKey:NSNumber.init(value:1),AVLinearPCMbitDepthKey:NSNumber.init(value:16), AVEncoderAudioQualityKey:NSNumber.init(value:AVAudioQuality.high.rawValue)]
    
    return settings
  }
  
  
  //04:10
  func preparedAudioRecorder(){
    let audioSession = AVAudioSession.sharedInstance()
    do{
      try audioSession.setCategory(AVAudioSessionPlayAndRecord)
      try audioRecorder = AVAudioRecorder(url:URL(fileURLWithPath:self.audioFileLocation()),settings:self.audioRecorderSettings())
      audioRecorder.prepareToRecord()
    }catch{
      print(error)
    }
  }
  
}
```

