Application Concepts
====================

.. _application_concepts-code_separation:

Code Separation
---------------

Although it is very easy in JavaScript to have a major code mess, in an application
written entirely in JavaScript it is essential that code is strictly ordered.

There are multiple separation criteria in myArmy:

#. Separate code from data.

   There is no game data defined in JavaScript, but only in JSON. So data is always
   passive and not executed (the - quite huge - exception to this rule is that there
   are expressions in the data which are evaluated as JavaScript code; this code is
   included in the game data).

#. Separate logic, data and display from each other.

   The game data is being loaded into model objects, which are themselves passive
   data holders and include close to no executed code (only very limited functions
   on their internal state).
   
   The game data is manipulated in objects and functions that themselves hold neither
   own data nor change the GUI. There are (global) state variables that hold the 
   entire application state. No information is stored in or taken from the DOM tree.
   
   The game data is displayed in specialized GUI objects that react to state changes.
   
   Approximately this is an implementation of the Model-View-Controller design pattern.

#. Separate function calls.

   myArmy makes heavy use of events. This way, code can be decoupled completely from
   other code by removing the need to call functions in other objects.

#. Encapsulate functionality in extensions.

   An extension system is provided, which encapsulates functionality in a few
   files within the extension directory. An extension can be plugged in and out in
   only two or three lines of code, thus providing a clear separation from the core
   code and other extensions. 

Objects
-------

myArmy is mostly implemented in an object-oriented way (and where it is not, it likely
will be in the future).

TODO

Data
----

TODO

State
-----

Application state is never stored in DOM elements, but in some state variables.
These state variables are global and always prefixed with an underscore.

Events
------

There are a few kinds of events used in myArmy (which all boil down to HTML events at the end).

#. HTML events.

   The events you know and love.

#. jQuery events.

   You might know and love these as well.

#. myArmy events.

   But you won't know these.
   There is an event dispatcher object named `_dispatcher`.
   Objects can register themselves as listeners for one or more events by calling
   `_dispatcher.bindEvent()`.
   
   Example: ::

    _dispatcher.bindEvent("postInit", this, this.onPostInit, _dispatcher.PHASE_STATE);
   
   This call tells the event dispatcher to add the calling object (second parameter)
   to the list of listening objects for the event `postInit` (first parameter). When
   the event is dispatched, the method `this.onPostInit` in the registered object
   instance will be called. The fourth parameter defines in which phase the registered
   method should be called. There are currently three phases for which objects can register.
   
   Begin Phase (`PHASE_BEGIN`)
   
   Lacking of a better name, this is simply the first phase in which events can be registered.
   Register your method in this phase if you want to prepare data needed in the following
   phases.
   
   Action Phase (`PHASE_ACTION`)
      
   Register your method in this phase if you want to change the application state after a
   user action. This phase is typically used by constraint checkers, army link manipulators and so on.
   
   State Phase (`PHASE_STATE`)

   Register your method in this phase if you want to use the data changed in the previous
   phases. This phase is typically used by render actions.

   An event name always starts with a prefix `pre` or `post`. This defines when an event
   is being dispatched - e.g. `preChangeArmy` might be dispatched when the process of 
   changing an army is initiated but no work is done yet. `postChangeArmy` might be
   dispatched after the army change work is done. Note that not every event is implemented.
   (currently there is an actual `postChangeArmy` but no `preChangeArmy` event).
   See :ref:`appendix-available-events` for a list of supported events.

   Note that after a user event there might be multiple events - be it that a method triggers
   more than one event, or a method called by the event dispatcher triggers an event itself.
   When dispatching and consuming events, be sure to not create an endless event cycle.
   
   
   