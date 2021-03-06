# nictalk
npm module for TTS with NICT

[![NPM](https://nodei.co/npm/nictalk.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/nictalk/)

[![Build Status](https://travis-ci.org/chokihub/nictalk.svg?branch=master)](https://travis-ci.org/chokihub/nictalk)
[![npm version](https://badge.fury.io/js/nictalk.svg)](https://badge.fury.io/js/nictalk)
[![Code Climate](https://codeclimate.com/repos/5873bfe4d977d62336001f6a/badges/1077f22d0c74e475197b/gpa.svg)](https://codeclimate.com/repos/5873bfe4d977d62336001f6a/feed)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

### About nictalk
Node.js上で動作する音声合成モジュール  
<br />
You can use TTS.  
All processes of TTS (text to speech) are combined into only one command.  
This module relies on [NICT](http://komeisugiura.jp/software/software_jp.html) for sounds generation from text.
And speech section is the diversion of the code of [simplayer](https://www.npmjs.com/package/simplayer).  
Each technology belongs to them, respectively.  
<br />

### Install
Before use this, you need to build an environment to play sound.

```npm install nictalk --save```

when you make the path, nictalk can be used on not only Node.js but also command line.
<br />

### Usage

####On Node.js
This is a basic source. Only run `node app.js`.

```Javascript:app.js
var NICTalk = require("nictalk");

var speaker = new NICTalk();

speaker.speak("voice", "Hello world.", function(error){
	if (error) throw error;
	console.log('End of Speech.');
});
```

When it succeeds, "voice.wav" is created in the current directory. And the sound "Hello world." be played.  
<br />
In the above example, speaker holds the following members basically. You can change them as necessary whith json.

```
var defaultParams = {
	"version" : "1.1",
	"language" : "ja",			//Japanese(ja), Chinese(zh), Korean(ko) or English(en)
	"voiceType" : "*",				
	"audioType" : "audio/x-wav",
	"directory" : ""			//Current Directory
};
```

These parameters can be changed with following method.

```
setParams(json);		ex)setParams({"language" : "en", "directory" : "/home/voices"});

setLanguage(lang);		ex)	setLanguage("en");

setDirectory(path);		ex)	setDirectory("/home/voices/");
```

<br />
Below is the syntax of the method speak.  

```
speak(file, [text], [callback]);
```

"text" and "callback" can be omit.
when "text" is omit, it only play "file";
"file" specify the file name (in the current directory) or path.
This file's path is shaped like `"directory"+"file"+".wav"`.  
<br />
it can practically use like this.

```
var NICTalk = require("nictalk");

var Japanese = new NICTalk();

var English = new NICTalk({"language" : "en", "directory" : "./english/"});

var Chinese = new NICTalk();
Chinese.setParams({"language" : "zh", "directory" : "./chinese/"});

var Korean = new NICTalk();
Korean.setLanguage("ko");
Korean.setDirectory("./korean/");

Japanese.speak("voice", "こんにちは", function(){
  English.speak("voice", "Hello", function(){
    Chinese.speak("voice", "你好", function(){
      Korean.speak("voice", "안녕하세요");
    });
  });
});
```

####On command line

This module can be used on command line.  
In this case, you have to global install this module.  

```npm install nictalk -g```  

The command is below.

```nictalk 'file' [text]```

This works exactly the same as `speak(file, [text]);`.

```
ex)	nictalk /home/voices/hello Hello.
```
<br />

###LICENSE

####MIT
