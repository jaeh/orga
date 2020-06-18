# interspace.chat

## Todos:

### Component hierarchy

think through the various component abstraction layers,
for example

* Space -> Room -> Popups
* Popups -> IframeProvider -> Iframe

### State

Figure out hidden state in the react app,
move it into one global state.
* youtube stream links
* discord tokens
* etc

### pretalx api connection

connect to our pretalx instance and get speakers and conference schedule from there.

+ figure out how to save all config in pretalx (or not)
  ***actually, let's not.***
  the config tells us where the pretalx instance lives, if there is one,
  so it should be separated, just start fetching data from it, if it exists
