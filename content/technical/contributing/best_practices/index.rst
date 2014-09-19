Best Practices
==============

Please follow these guidelines when contributing code.
When contributing a new extension, please do also read and follow the :doc:`/content/technical/extensions/introduction/index` chapter.

Respect Copyrights
------------------

As myArmy is a utility for gaming systems created by commercially acting companies,
it uses the publications of those companies as "data sources". If myArmy should ever
provide almost complete rules written in these publications, they will sell less
items and will (by right) defend their copyright. So you must not add functions that
render the original publications useless. For example, it is not allowed to add
rule explanations or model profile values.

Respect Privacy
---------------

Features that violate the user's privacy are not allowed.

Keep it Simple
--------------

myArmy is and should stay a relatively light-weight system that offers quite easy
access to new users and quick response times. So everything that adds complexity for
users and developers must also add a significant improvement.

Keep it Small
-------------

myArmy is often used on mobile devices. So please keep download sizes as small as 
possible to ensure short loading times. Do not rely on heavy-weight 3rd-party
libraries only to use a fraction of their functionality (this is for example the reason
why no fancy UI frameworks like Bootstrap or jQuery UI are used).

Keep it Independent
-------------------

While myArmy currently only supports a single game system, it is intended to be an all-system
tool (or at least to be extendable in the future). So do not tailor a concept entirely to 
a specific game system. If you want to name a variable or function after a game concept, 
you're likely to do it wrong.

Separate Code
-------------

Please see :ref:`application_concepts-code_separation`.

Keep it Optimizable
-------------------

Limitations in the HTTP protocol make it inefficient to load lots of files on the client
side. It is much more efficient to combine files so that there is a minimum number of
files for the browser to load. Contributions need to ensure that myArmy can be used with
or without such an optimization without needing code changes (except differing link and
script tags).

Code Conventions
----------------

Please see the existing code as a guideline for code conventions (naming, formatting, etc.).
