# Jitsi Meet Chrome Crash

This is a sample project that demonstrates Google Chrome crashing when moving an `<iframe>` element
of a [Jitsi Meet]([url](https://meet.jit.si/)) video call is moved between the slots of a
[Web Component]([url](https://developer.mozilla.org/en-US/docs/Web/API/Web_components)).

The issue seems to be widespread on Chromium-based browsers since it was also reproducible on [Arc]([url](https://arc.net/)).

Check this demo video:

https://github.com/LSViana/jitsi-meet-chrome-crash/assets/21217790/632250d9-ab4e-4fc2-8b0c-9d62c73b354f

The demonstration video shows the browser crashing when focusing the "Name" input inside of the `<iframe>`
but sometimes the browser crashes without requiring any user interaction.

For more information, I recommend to:

1. Access [jitsi-meet-chrome-crash.vercel.app]([url](https://jitsi-meet-chrome-crash.vercel.app/)) to try and reproduce the issue locally;
   - Save your work before trying this since your browser may crash.
   - You may do it by cloning the repository into your machine as well.
   
2. Check the source code inside `src/components/Demo.vue` where the code that causes the crash lives.
