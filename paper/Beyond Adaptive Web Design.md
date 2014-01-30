# Beyond Adaptive Web Design

## Introduction

The Web is continually evolving and we need to evolve with it.

It used to be easier to manage browsers when there were just a few of them on the desktop. Today we not only have to deal with a wide range of desktop browsers but mobile devices, tablets, and more. Even for the average site things have changed a lot over four years: browser share, operating systems, screen resolutions, and more. [User Interface 17]

While creating flexible layouts is important, there’s a whole lot more that goes into truly exceptional adaptive web experiences. This session will introduce the Principles of Adaptive Design: ubiquity, flexibility, performance, enhancement and future-friendliness. [Beyond Squishy: The Principles of Adaptive Design]

The power of the web is its ubiquity. No one knows what the landscape is going to look like in a couple years, but there’s a damn good chance the gadgets sitting underneath Christmas trees a few years from now will have access to the web.
Because of this, we need to preserve and embrace the web’s ubiquity. This requires us to deliver full web experiences regardless of how people access the web.

Continue creating flexible interfaces that can adapt to any screen size. Performance often takes a back seat to everything else. Progressive enhancement, feature detection and many other techniques allow us to build up a core experience that allow us to support more devices while still optimizing for the the best of the best.

The key aspect of Future Friendly thinking is to acknowledge and embrace unpredictability. Again, nobody knows where things are going and the one thing we can count on is change.

Adaptive web design is essentially progressive enhancement at its core, but it’s being applied to a much larger, more diverse landscape than when the term progressive enhancement was first coined. We now have Web-enabled smartphones, tablets, e-readers, netbooks, watches, TVs, phablets, notebooks, game consoles, and a whole bunch more.

Responsive design is one technique in an adaptive web design strategy. Creating flexible layouts is extremely important, but it’s just one piece of the puzzle. It’s also important to consider a whole host of other factors as well: ergonomics, touch capability, geolocation, SVG support, and the myriad other features that can be detected.

I’d personally like to see “adaptive design” become synonymous with creating a single Web experience that modifies based on the capabilities of the device and browser. Website can access superpowers in devices.

### Adaptive Input methods

Web browsers on TVs are actually might better than you might think but the input is terrible so no one uses them. Input is much more important to interface design than screen size. The input defines what a design needs to do in order to accomplish a task. At every form factor we see touch, cursors, and keyboards available for input. [Adaptive Input]

The current Glass interface is limited to a floating rectangle above your head. You don’t have full range of motion and, as a result, no spatial cues or depth in the interface.

There is no one true input for the Web. We have to contend with fingers, mice, keyboards, and more.

#### Touch

Touch is no longer just isolated to smartphones and tablets. Every desktop design has to be touch-friendly now.

The optimal touch target size is 7mm, based on the average size of human finger tips and pads. CSS2.1 defines a pixel as 1/96 of an inch. So 7mm should be 30pixels. However, things aren’t so easy because of dynamic viewports. [Designing for Touch]

The best touch interface is sometimes no touch at all. Using sensors and speech is the next frontier for interaction design. This is no longer science fiction but reality. The challenge for us over the next few years is not designing for one input but many.

#### Speech

#### Device motion

Device motion is made possible by a combination of always-on sensors (typically an accelerometer, a magnetometer, and a gyroscope) that tell us how a computer is moving through the space around it. The ability of these sensors to provide precise information about the movement of a device opens up new design possibilities for applications. From adjusting the user interface based on orientation changes to using three dimensional motion as input, to combining device motion with location detection, video cameras, and light sensor capabilities, there's no shortage of interesting interface designs made possible by Device Motion. [Re-imagining Apps for Ultrabook]

Device motion sensors can tell us a lot about how a device is moving in someone’s hands but they can also clue us in to environmental changes as well.

#### User Motion


### Adaptive Web Components

One of the most common critiques against responsive Web design is that it creates large (file size) Web sites, thereby slowing Web pages down. But we can make responsive sites perform well, we just have to the work to make it possible. [20MB Responsive Websites]

We care about mobile performance because people need fast experiences on the Web. There's lot of studies that highlight the importance of speed. More than half of people with a bad loading experience on mobile, won't come back.
Speed is a feature. You can quantify its impact on the metrics you care about. [High Performance Browser Networking]

We all should care about page speed. 73% of mobile internet users say they've encountered Web pages that are too slow. A 1 second delay can result in a 7% reduction in conversions.
Mobile network speeds have gone up but this doesn't help much as page load times tend to plateau as bandwidth increases. Latency is a much bigger contribution to download times. LTE reduces tower latency by several milliseconds but we still need to make a number of connections to get data to your phone. [Page Speed is Only the Beginning]

Web components allow you to use custom HTML elements in the browser. You can wrap up a simple element or an entire application within an HTML element. Web components allows you to build Web applications in a modular, reusable, and encapuslated way.

## Evaluation and experiments 

### Input methods

### Components

So what are we to do? This is actually a great opportunity to utilize conditional loading to serve the best experience for the right context.

A static default. We can then use Javascript to detect when it’s appropriate to introduce the embedded map. After all, embedded maps work quite well when there’s enough room to maneuver within them. We can simply replace the default experience with the iframe map when enough screen real estate becomes available.

By default we can simply include a text link to the location on the Google Maps website. And in case a “View Map” text link isn’t attractive enough for you, we can also use the Static Maps API to pull in a static image of the location.

When a user taps the link, most major mobile platforms will fire up the native maps application where the user can have a richer experience. If the native experience is unavailable, the user is simply taken to the Google Maps website, where they receive a dedicated full-screen mapping experience. Either way, it’s a better experience than a cramped embedded map.

This approach works quite well for simple map plotting and even showing groups of locations. However, more interactive mapping requires additional consideration, but even then I’d say that an embedded map still might not make sense. While techniques like adaptive maps might not make sense in every circumstance, it’s a decent baseline.

## Conclusion

More changes are coming, new APIs and beyond. What will you do with this new power? An innovator is someone who wakes up to the constraints caused by false assumptions, and breaks out of them.

## Refereneces

1.  Luke Wroblewski - Mobile First. ISBN: 978-1-937557-02-7
2.  Luke Wroblewski - Re-imagining Apps for Ultrabook. Intel Software 2013
-   Ethan Marcotte - Responsive Web Design. ISBN: 978-0-9844425-7-7
-   Jason Grigsby - Adaptive Input. Breaking Development in San Diego CA 2013
-   Brad Frost - Beyond Squishy: The Principles of Adaptive Design. SXSW conference, Austin, TX, USA 2013
-   Aaron Gustafson - Building Adaptive Designs Now. User Interface 17, Boston, MA 2012
-   Mat Marquis - 20MB Responsive Websites. Breaking Development in Orlando FL 2013
-   Josh Clark - Designing for Touch. An Event Apart in Seattle, WA 2013
-   Ilya Grigorik - High Performance Browser Networking, ISBN: 9781449344764 O'Reilly Media, Incorporated. 2013
-   Peter McLachlan - Page Speed is Only the Beginning. Breaking Development in San Diego CA 2013
-   Basson, Sara and Fairweather, Peter G. and Hanson, Vicki L. - Speech Recognition and Alternative Interfaces for Older Users. ACM 2007
-   Kratz, Sven and Rohs, Michael and Essl, Georg - Combining Acceleration and Gyroscope Data for Motion Gesture Recognition Using Classifiers with Dimensionality Constraints. Proceedings of the 2013 International Conference on Intelligent User Interfaces. 2013
  





   

