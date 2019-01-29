# oojs-clock
This showcase object oriented JavaScript project uses three APIs to show the user current location's time and show local photos taken.

The first API  ([ipstack](https://ipstack.com/)) retrieves the location of the user based on her IP.

The second API([[timezonedb](https://timezonedb.com/)]) receives the parameters that were retrieved from the IP and uses them for the _longitude_ and _latitude_.

The third API ([flickr](https://www.flickr.com)) also uses the location data to retrieve relevant photos from the user's location.

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn run serve
```

### Compiles and minifies for production
```
yarn run build
```

### Lints and fixes files
```
yarn run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
