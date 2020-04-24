## Home Assistant Configuration

Most of the config from my Home Assistant setup is here.  However, I now use the gui for configuring some elements such as integrations and helpers.  I also have most of my automation in Node-Red so you won't find the whole story in these files. 

### Lovelace

Lovelace is great, but until recently, I found it very hard to get the views I wanted on both a widescreen PC and a mobile phone, usually used in portrait orientation.

Building something that meant you weren't always scrolling about on a small screen, usually meant not making full use of the larger screen.  Put more information on a large screen and the key items you want on the phone were often hidden away.

I used [Custom Header](https://maykar.github.io/custom-header/#intro/intro) to change the views displayed on different screens but never quite got what I wanted.  Plus, maintaining seperate views for different devices was a PITA.

When Home Assistant v107 brought us Dashboards I decided to rethink my whole Lovelace configuration and make it more DRY for easier maintainability.

What I have here might seem complicated, but pretty much everything is defined once and reused where it's needed.  This makes it really easy to make a tweak or add a feature.  The approach is also very modular so I can be reasonably sure that hanging one thing doesn't introduce odd bugs elsewhere.

### The Approach

Much like it is usually good to split code into reusable functions, I've chosen to split yaml configuration into reusable chunks in seperate files, which are included where needed.  I call these cards, although they may actually consist of a number of cards, with borders removed to appear like one.

The structure is :

- a dashboard file for each device - very little in here
- device specific view files inclued in the relevant dashboard - mostly this is about layout and control
- card files included in the view files, these are share between several views / devices as required - all the 'clever' stuff lives in these

The dashboard files are in the root of the config folder (annoyingly, you can't move them).  All other files live in a viewfiles folder and are named to avoid too much confusion.

To get an idea of the output, check the screenshots folder, I'll try to keep it reasonably up to date and naming should follow the view files.

### Some of the custom stuff I use to make it work
- https://github.com/thomasloven/lovelace-layout-card - lets's you put cards where you want to. I use grid layout a lot for PC views and for placing individual cards in combinations.
- https://github.com/thomasloven/hass-lovelace_gen - template cards, pass variables, massively reduce duplication.  There's too much to say about this card, I've barely scratched the surface with it.  However, lovelace_gen is not dynamic and has no access to states (it's basically creating a set of lovelace files behind the scenes).
- https://github.com/iantrich/config-template-card - so I use this card for dynamic state changes and manipulating cards based on states data.
- https://github.com/thomasloven/lovelace-card-mod - lots of uses for this, from hiding card elements based on state, removing borders and shadows (where the next card isn't perfect), to coloring, flashing, resizing and repositioning elements to meet my fussy nature.
- https://github.com/custom-cards/stack-in-card - good for creating horizontal or vertical stacks with no borders.

### Some of the custom stuff I use to make it nice :-)
- https://github.com/maykar/custom-header
- https://github.com/thomasloven/lovelace-slider-entity-row
- https://github.com/kalkih/mini-graph-card
- https://github.com/kalkih/mini-media-player