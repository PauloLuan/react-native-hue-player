# react-native-hue-player

HUE Player is intended to projects that need to deal with both offline/local and online/streaming audio.
Now you can play, pause, skip and seek audios from diferent sources on the same playlist.

This project is based on ['ract-native-audio-streamer'](https://github.com/indiecastfm/react-native-audio-streamer),
['react-native-sound'](https://github.com/zmxv/react-native-sound) and uses ['react-native-music-control'](https://github.com/tanguyantoine/react-native-music-control).

![print](/Example/prints/print1.jpg)
## Getting Started

In order to use this component you have to set up a playlist of audio files. Those audio files must have some attributes, as shown on the schema bellow: 

```js
const playlistSample = [
  {key: 'audio01', title:'Irineu', url: 'http://vocenaosabe.nem/eu.mp3'}, 
  {key: 'audio02', title:'SerjaoBerranteiro', url: 'http://aquitem.corage', path: 'matadorDeOnca.mp3'}
];
```
Note that the audio objects may have other fields, but "key", "title" and "url" are required.
By default the first track to be played is the first one on playlist array.

### Installing

Install on your project root using:

```shell
yarn add react-native-hue-player
```
or

```shell
npm install react-native-hue-player
```

This component is based on three other projects, so make sure you run the commands to link Android and iOS.

```js
react-native link react-native-audio-streamer
react-native link react-native-sound
react-native link react-native-music-control

```
### Usage

All you need to control your audio files is provided by the AudioController class, but if you want to use or customize our ready-to-go interface you can import the AudioControls component.

#### AudioControls

Basic usage:

```js
import { AudioControls } from 'react-native-hue-player';

...
<AudioControls
  initialTrack={1} // starts on second audio file
  playlist={playlistSample}
/>

```

Props:

|             Name              | Type              | Default       | Description                                                                            |
| ----------------------------- | ----------------- | ------------- | -------------------------------------------------------------------------------------- |
| activeColor                   | color             | '#FFF'        | Main color of the compontent, used as default when buttons are active                  |
| inactiveColor                 | color             | '#888'        | Secondary color of the compontent, used as default when buttons are inactive/disabled  |
| hasButtonSkipSeconds          | boolean           | false         | Does you player has buttons to skip secods?                                            |
| timeToSkip                    | integer           | 15            | How many seconds you want your skip on your buttons                                    |
| thumbnailSize                 | image style props | -             | Size of the cover thumbnail                                                            |
| titleStyle                    | text style props  | -             | Custom style for the audio title                                                       |
| authorStyle                   | text style props  | -             | Custom style for the author name                                                       |
| activeButtonColor             | color             | activeColor   | Custom color for the buttons (play, pause, skip...) when they are active               |
| inactiveButtonColor           | color             | inactiveColor | Custom color for the buttons (play, pause, skip...) when they are inactive/disabled    |
| sliderMinimumTrackTintColor   | color             | activeColor   | Custom color on the left side of the slider                                            |
| sliderMaximumTrackTintColor   | color             | activeColor   | Custom color on the right side of the slider                                           |
| sliderThumbTintColor          | color             | activeColor   | Custom color of the slider circle                                                      |

#### AudioController

If you don't want to use our component you are free to implement one of your own. The AudioController is a singleton class that provides data from the current audio, including its status, and functions to manipulate the playlist and to control the player.

To use the AudioController class just import it on your component (if you do it in more than one component it will be the same instance).

```js
import { AudioController } from 'react-native-hue-player';

...
function wheneverYouNeed(){
  AudioController.init(playlistSample, initialTrack, this.onChangeStatus, this.updateCurrentTime);
}

```

| Function | Params | Descriptions|
|----------|--------|-------------|
|init | playlist: array, track: integer, onChangeStatus: function, onChangeCurrentTime: function | Initiate the audioController with the given playlist. Has optional initial track and two callback functions, called when the audio status changes and every second when currentTime changes.


### Example

The project is linked already.
