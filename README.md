# Docker PHP image for CI


## Use cases

### PHPCS

```
phpcs --version
phpcs --standard=PSR2 src/
phpcs --standard=.phpcs.xml src/
```

### PHPMD

```
phpmd --version
phpmd src/ text cleancode,codesize,controversial,design,naming,unusedcode
phpmd src/ text .phpmd.xml
```

### PHPCPD

```
phpcpd --version
phpcpd src/
```

### PDEPEND

```
pdepend --version
pdepend --jdepend-xml=/tmp/pdepend.xml .
```
