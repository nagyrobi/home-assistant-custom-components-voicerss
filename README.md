This is a fork of Home Assistant's built-in VoiceRSS component as a custom component, with extra options :
- prepending a silence delay to the audio stream
- speech rate (aka speed)
- language voice (if your language has more to choose from)

Many people complain about network media players cutting down the first bits of the TTS audio because their devices need a little time to wake up from standby or idle state when they receive a network stream to play. The only good solution for this is to add a configurable amount of silence at the beginning of the audio stream. The proposed solution does this locally, and the generated files stay like that in the cache.

I submitted this as a PR originally, but they rejected it because the component doesn't contain a config_flow, well, all I did was to add two more options to the config, but I didn't engage into rewriting the whole thing just because somebody didn't create a flow for it - nevertheless, the component still functions as is.

Adding this as a custom component to your Home Assistant instance will override the internal component with the same name so you can still use it as before, with the extended functionality as below.

The `voicerss` text-to-speech platform uses [VoiceRSS](http://www.voicerss.org/) Text-to-Speech engine to read a text with natural sounding voices.

## Configuration

To enable text-to-speech with VoiceRSS, add the following lines to your `configuration.yaml`:

```yaml
# Example configuration.yaml entry
tts:
  - platform: voicerss
    api_key: YOUR_API_KEY
    language: en-gb
    codec: aac
    format: '44khz_16bit_mono'
    speed: '-2'
    voice: Nancy
    delay: 1000
```
Configuration options:
```
api_key:
  description: The API Key for VoiceRSS.
  required: true
  type: string
language:
  description: The language to use.
  required: false
  type: string
  default: "`en-us`"
codec:
  description: The audio codec.
  required: false
  type: string
  default: " mp3 "
format:
  description: The audio sample format.
  required: false
  type: string
  default: " 8khz_8bit_mono "
voice:
  description: The voice name for the selected language. If unconfigured, uses the default voice set by VoiceRSS.
  required: false
  type: string
  default: unconfigured
speed:
  description: The rate of the speech (speed of talk). Valid values are " -10 " to " 10 ". Value needs to be in quotes.
  required: false
  type: string
  default: " 0 "
delay:
  description: "Prepend the generated speech with this amount of silence (miliseconds)."
  required: false
  type: int
  default: 0
```

With the `delay` option you can add some silence to the beginning of the rendered speech, to cope with audio systems which need time to wake up their speakers when starting a network stream. Value is in miliseconds, maximum is 15000 (15s).

When `delay` is set, the audio stream is sent to the player in uncompressed `wav` format to preserve audio quality (avoid recompression). Without `delay` set, the stream is sent unmodified, in its original format.

Check the [VoiceRSS API documentation](http://www.voicerss.org/api/) for language-specific voice values.

Please note, some media_players require a certain format. For example Sonos or Linkplay require a format of '44khz_16bit_stereo'.
