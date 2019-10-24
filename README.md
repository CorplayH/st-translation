# Straker Translations exercise

Github link :[st-translation](https://github.com/CorplayH/st-translation.git)

### Technologies/Frameworks used:

Vue.js (https://vuejs.org/)

CoreUI ([https://coreui.io/ ](https://coreui.io/ )-- free version)

### Goals achieved

- [x] Retrieve users from API and display 
- [x] Retrieve Articles from API and display 
- [x] Pagination
- [x] Search user by user name

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

## Project structure 

This project is bulit based on <span style="color:red">CoreUI</span> framwork and <span style="color:red">Vue.js. use <span style="color:red">Axios</span> as API request tool. 

By trim down the CoreUI framwork the final project includes:

1. One base structure folder (Src -> containers)
2. Three folders contains : Dashboard page, User page and Articles page  in (Src -> views)
3. Vue-router file "index.js" in (Src -> router)
4. Side menu is rendered by _nav.js.

## Key functions 

#### Fetching APIs:

```javascript
// fetch all user from API in file Src -> Views -> users -> Users.vue
getUserInfo() {
  this.axios.get('https://jsonplaceholder.typicode.com/users')
    .then((res) => {
    this.users = res.data;
  })
    .catch(error => {
    console.log(error.response)
  });
},
```

```javascript
// fetch single user from API by ID in file Src -> Views -> users -> User.vue
getUserInfo() {
  // this.$route.params.id to get params from url
  this.axios.get('https://jsonplaceholder.typicode.com/posts?userId=' + this.$route.params.id)
    .then((res) => {
    this.items = res.data;
  })
    .catch(error => {
    console.log(error.response)
  });
},
```

```javascript
// fetch user's post by ID from API in file Src -> Views -> article -> Article.vue
getArticle() {
  // this.$route.params.id to get params from url
  this.axios.get('https://jsonplaceholder.typicode.com/posts/' + this.$route.params.id)
    .then((res) => {
    	this.article = res.data;
    })
    .catch(error => {
    	console.log(error.response)
    });
},
```

#### Search function

````javascript
// Apply filter to user property in data, code is in Src -> Views -> users -> Users.vue
data: () => {
  return {
    users: [],
    search: ""
  }
},
computed: {
  filteredList() {
    return this.users.filter(user => {
      // search in user while typing
      return user.name.toLowerCase().includes(this.search.toLowerCase());
    })
  }
},
````

## Summary

This is a fun exercise, it took me about an hour to get to know the CoreUI framwork, and it's functions such as Tables, Menus.

Once I find out the structure of this framwork, I started to trim down the framwork, deleting unnessary code and resources, and get my UI done.

After this, I installed Axios from npm to fetch api data as the requirment  and apply to data to the UI framwork. 

After all the requirment are complete, I feel is good to have little search function to enhance the project a bit, so I use the  .filter & . includes functions from Vue to complete is task.

The most challenge part for me is in a limited time to use an UI framwork I never used before, and I am happy with my result.