Army Concepts
=============

State Machine
-------------

TODO (always states, no active actions in army data)

Option Lists
------------

TODO

Minimum and Maximum Selections
------------------------------

TODO

Pools
-----

TODO

Army Links
----------

TODO

The system registers a hashchange event listener. This way it can recognize the user
selecting a saved bookmark (browsers won't reload the page if a bookmark only differs
in its hash from the current page).
When setting the new hash after a state change, we need to deactivate the hashchange listener for a short time.
This is done in Persistence.createStatelink(). We even need to reactivate the event using
window.setTimeout() to avoid triggering the event instantly (better solutions are welcome).

Browser Compatibility
---------------------

While browser compatibility isn't too great a problem on desktop systems, mobile browsers
are now major sources of flipped desks.
myArmy detects the user's browser during initialization and uses replacements for the
"click" event on some browsers (which effectively means touch support). If we use touch
events, we need to ensure that the user didn't want to scroll. To achieve this,
we listen to touchEnd events and only assume a click if the touch start position and 
the touch end position are close enough to each other (see wasClick() method in guimobile.js).