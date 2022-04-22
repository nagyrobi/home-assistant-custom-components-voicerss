# VoiceRSS TTS - with extra prepending delay, speech rate and language voice

This is a fork of Home Assistant's built-in Google Translate Text-to-Speech component as a custom component, with extra options added:
- prepending a silence delay to the audio stream
- speech rate
- language voice (if your language has more to choose from)

Many people complain about network media players cutting down the first bits of the TTS audio because their devices need a little time to wake up from standby or idle state when they receive a network stream to play. The only good solution for this is to add a configurable amount of silence at the beginning of the audio stream. The proposed solution does this locally, and the generated files stay like that in the cache.

See the repo's readme for details.
