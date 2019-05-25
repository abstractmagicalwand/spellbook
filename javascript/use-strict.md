# "use strict"

For a long time, JavaScript evolved without compatibility issues. New features were added to the
language while old functionality didn’t change.

That had the benefit of never breaking existing code. But the downside was that any mistake or an
imperfect decision made by JavaScript’s creators got stuck in the language forever.

This was the case until 2009 when ECMAScript 5 (ES5) appeared. It added new features to the language
and modified some of the existing ones. To keep the old code working, most modifications are off by
default. You need to explicitly enable them with a special directive: "use strict".

1. The "use strict" directive switches the engine to the "modern" mode, changing the behavior of
some built-in features.
2. Strict mode is enabled by placing "use strict" at the top of a script or function. Several language
features, like "classes" and "modules", enable strict mode automatically.

## Details

- [The modern mode, "use strict"](http://javascript.info/strict-mode#use-strict)
