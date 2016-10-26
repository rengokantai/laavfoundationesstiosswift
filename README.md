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
  @IBAction func recordButtonPressed(sender:AnyObject){
    //07:20
    if !audioRecorder.isRecording{
      let audioSession = AVAudioSession.sharedInstance()
      do{
        try audioSession.setActive(true)
        audioRecorder.record()
      }catch{
        print(error)
      }
    
    }else{
      audioRecorder.stop()
      let audioSession = AVAudioSession.sharedInstance()
      do{
       try audioSession.setActive(false)
      }catch{
        print(error)
      }
      if(self.verifyFileExists(){
        playButton.isHidden=false
      }else{
        print("Error")
      }
    }
    self.updateRecordButtonTitle()
  }
  @IBAction func playButtonPressed(sender:AnyObject){
    
  
  }
  
  func audioFileLocation()->String{ return NATemporaryDirectory().appending("audio.m4a")}
  
  func audiorerderSettings()->[String:Any]{
    let settings = [AVFormatIDKey:NSNumber.init(value:kAudioFormatAppleLossless),AVSampleRateKey:NSNumber.init(value:44100.0),AVNumberOfChannelsKey:NSNumber.init(value:1),AVLinearPCMbitDepthKey:NSNumber.init(value:16), AVEncoderAudioQualityKey:NSNumber.init(value:AVAudioQuality.high.rawValue)]
    
    return settings
  }
  
  //06:01
  func updateRecordButtonTitle(){
    if audioRecorder.isRecording{
      recordButton.setTitle("Recording..",for:.normal)
    }else{
      recordButton.setTitle("Record",for:.normal)
    }
  }
  
  //06:35
  func verifyFileExists()->Bool{
    let fileManager=FileManger.default
    return fileManager.fileExists(atPath:self.audioFileLoaction())
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

###3 Introduction to AVAudioPlayer
```AVAudioPlayer``` allows you to play back audio from either a file or something that was captured and is still in memory.  

The only time you'd want to consider something else is either when you're dealing with streaming content or you have a requirement for really low latency I/O. When dealing with streaming content, you want to use the ```AVPlayer``` class to do the job.

####00:48
```
//single shot, or loop
AVAudioPlayer.numberOfLoops()
//play multiple files
AVAudioPlayer.playAtTime(time:)
AVAudioPlayer.volume
AVAudioPlayer.pan
AVAudioPlayer.rate
```

###4 Play back audio
AudioViewController.swift
```
//00:19
var audioPlayer:AVAudioPlayer!

//01:00
func playAudio(){
  let audioSession = AVAudioSession.sharedInstance()
  do{
    try audioSession.setCategory(AVAudioSessionCategoryPlayback)
    try audioPlayer = AVAudioPlayer(contentsOf:URL(FileURLWithPath:self.audioFileLocation()))
    audioPlayer.preparedToPlay()
    audioPlayer.play()
  }catch{}
}
@IBAction func playButtonPressed(sender:AnyObject){
    
  self.playAudio()
  }
```


