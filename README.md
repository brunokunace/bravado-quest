# Bravado Quest

### Comments
* Use virtual scroller for get the most performatic list and filter
* For highlight text, need to use v-html, but can lead to XSS attack
* I change the font-size to try adapt this design to mobile, but is not in figma

### Difficults found
* Highlight a text with case-insensitive, because need to change text to insert a `<mark>`, replaceAll not is best for it, need to create a regex like function, but i dont know if it is worth for this test 


## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```
