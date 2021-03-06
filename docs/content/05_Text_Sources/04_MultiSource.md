# MultiSource

Multisource is exactly what it's name indicates. It acts as a single source but is in fact
an aggregate of multiple source of texts.

When used, it will simply iterates over all of sources passed in it's constructor.
You are then responsible of the order the sources are iterated on.

```php
<?php

$misspellingFinder = new MisspellingFinder(
    Aspell::create(), // Creates aspell spellchecker pointing to "aspell" as it's binary path
    new EchoHandler() // Handles all the misspellings found by echoing their information
);

/** @var \PhpSpellcheck\Misspelling[]|\Generator $misspellings */
$misspellings = $misspellingFinder->find(
    new \PhpSpellcheck\Source\MultiSource(
        [
            new \PhpSpellcheck\Source\File(__DIR__.'/../tests/PhpSpellcheck/Tests/Fixtures/Text/mispelling1.txt'),
            new \PhpSpellcheck\Source\File(__DIR__.'/../tests/PhpSpellcheck/Tests/Fixtures/Text/Directory/mispelling3.txt')
        ]
    ),
    ['en_US'],
    ['from' => 'aspell spellchecker']
);
```
