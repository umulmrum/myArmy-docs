Introduction to Extensions
==========================

myArmy implements an extension system which allows to add functionality without having
to change the core code.
The system currently only has a few extension points - maybe we will need to add
additional hooks in the future.

Note: This chapter contains a lot of 'must' and 'should'. While this may sound a bit rude,
it ensures that the code remains readable and understandable, und thus maintainable.

Extension Structure
-------------------

An extension needs to comply with the following rules:

#. Choose a (simple) name for your extension. This name may only consist of lower-case characters, e.g. `summary`.
   This name determines most of the names of your extension files and objects.
#. There must be a sub-directory in the `extensions` directory with the extension name.
#. In this directory, a file with the extension name + `Extension.js` must exist, e.g. `summaryExtension.js`.
#. If your extension needs custom logic, it must be in a file named like the extension + `Logic.js`, e.g. `summaryLogic.js`.
#. If your extension needs a GUI, it must be in a file named like the extension + `Gui.js`, e.g. `summaryGui.js`.
#. If your extension needs CSS, it must be in a file named like the extension + `.css` e.g. `summary.css`.

You can add additional files, but please try to keep the number of files small.

Extension Object
----------------

The extension object is the main initialization object for an extension. It hooks into
the core application and starts the extension logic and GUI.
The extension object's name is the extension name + `Extension` (camel-case), e.g. `SummaryExtension`. It is defined in `summaryExtension.js`.
Do not include functionality in this object (except for simple callbacks for events).

TODO extension points and how to use.

Logic
-----

The extension logic must consist of a object named like your extension + `Logic` (camel-cased), e.g. `SummaryLogic`. It is defined in `summaryLogic.js`.
It should contain a method `init()` which is used to initialize the logic (well .. :-) ).
The logic's responsibility is to handle any actions or calculations the extension needs to perform.
The logic must not contain rendering functionality (simply said, never include any access to the DOM tree here, nor to 
anything defined in a GUI object).

GUI
---

The GUI must consist of an object named like your extension + `Gui` (camel-cased), e.g. `SummaryGui`. It is defined in `summaryGui.js`.
It should contain a method `init()`, in which events for rendering are registered.
The GUI may only react to events - GUI methods may not be called directly.
The GUI must not contain logic and must not save application state (except strictly GUI-related state).
If your extension needs images, they must be located in a sub-directory `img`. Images may
not be included in `<img>` tags, but only in `background-image` CSS declarations (this
enables a build process to optimize files and still find all images).

Translations
------------

Extensions must be fully translatable if they infer texts. They may not hard-code texts that are seen by the user.
Currently there is no extension point for translations. Therefore translations need to be
included in `textcommon_en.json` (and the equivalent files in other languages).

Integration
-----------

To integrate a new extension into the core system, do this as follows:

#. Add all JavaScript files that need to be loaded in `myArmy.js`.
#. Add all CSS files that need to be loaded in `myArmy.css`.
#. Add the extension object in the `extensions` array in `core/options.js`.
#. If your extension needs translations, add them to `textcommon_en.json` and all equivalent
   files in other languages. You don't need to translate all texts yourself, but the
   text needs to be in all language files (put the English text in every `textcommon_xx.json` 
   if unsure).

These are the only locations where an extension may modify the core code (there are 
exceptions to this rule in old code - this is to be refactored in the future).

Documentation
-------------

Please provide some documentation by adding it to the :doc:`/content/technical/extensions/index` chapter of this documentation project.

TODO
what to document