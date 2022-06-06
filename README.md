# Facade

## Learning Goals

- Explain the facade pattern
- Use the pattern in Java

## The Facade Pattern

Use the Facade pattern when there is complex functionality that you want to
simplify so it's easier for client classes to use that functionality and the
complexity can be abstracted away.

Highlights of the Facade pattern:

- Abstraction to simplify a complex system
- Optional - a facade can be used or the underlying components of the more
  complex system can be still be used individually - we will experience this
  when we implement a digital version of our camera
- A facade should not add logic of its own - it's just a simple interface to
  existing functionality
- Internal workings of the facade are not exposed to client systems

You may not have realized it, but we used this pattern already in our Camera
lab. The `takePhotograph()` method in our `Camera` class does nothing but put
together a series of calls to leverage existing functionality in other classes:

```java
        filmOps.engageFilmMechanism();
        filmOps.rollFilm();
        filmOps.releaseFilmMechanism();

        mirrorOps.openMirror();;

        shutterOps.setShutterSpeedSetting(shutterSpeed);
        shutterOps.initializeShutter();
        shutterOps.activateShutter();
        shutterOps.releaseShutter();

        mirrorOps.closeMirror();
```
