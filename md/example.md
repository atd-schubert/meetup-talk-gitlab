## Markdown


### Unordered List

* Lorem
* Ipsum
* Dolor
* Sit
* Amet


### Ordered List

1. Lorem
1. Ipsum
1. Dolor
1. Sit
1. Amet


### Source-Code (Bash)
```bash
#!/bin/bash

###### CONFIG
ACCEPTED_HOSTS="/root/.hag_accepted.conf"
BE_VERBOSE=false

if [ "$UID" -ne 0 ]
  then
  echo "Superuser rights required"
  exit 2
fi

genApacheConf(){
  echo -e "# Host ${HOME_DIR}$1/$2 :"
}
```


### Source-Code (JavaScript)
```javascript
Mapbender.on(event, function() {
    alert('Now!');
});
```


### Source-Code (PHP)
```php
class Mapbender {
    public majorVersion = 3;
}
```


### Speaker Notes

This is public

Note: This is private
