# Making a Basic Teachers list with 

We're going to create a small application with Vue. The app will be a simple Becode teachers database.

Today we will learn:

-   How to  set up  Vue
-   The  anatomy of a Vue file
-   How to work with  data, methods, conditional statements, and events  in Vue

We will also refresh some things we learned before in the course:

-   How to  create, update, view, and delete teachers from the system 
-   How to  make API calls  for each of the above actions
-   How to use  form  validation


## 1. What is Vue?

-   Vue (or Vue.js) is an open-source front-end JavaScript framework
-   Vue is the  **view**  layer of an MVC application (Model View Controller)
-   Unlike other popular JavaScript projects, Vue is not backed by a large company like React (Facebook) or Angular (Google). 
- Vue was originally written by  [Evan You](https://github.com/yyx990803)  and the open-source community.

## Setup and Installation

There are two main ways to set up Vue - in a Node project, or directly injected into a static HTML file. I'd first like to take a look at setting up Vue in an HTML file, as it's the simplest setup and introduction. Those who have only ever used a library like jQuery will be most familiar with this method. If you've already used React or another JavaScript framework, feel free to skip to the next section.

We can just create a basic HTML file and add a link to a Vue CDN in the head, and create a  `<div>`  with an id of  `app`.

### Static HTML File

index.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <title>Vue App</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

We can create a simple "Hello World" with Vue. Using double brackets, we'll render  `message`  in  `app`. In the  `<script>`  tag, we'll link the data and the DOM. We create a new  `Vue`, and the  `message`  property on  `data`  will be rendered.

index.html

```html
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

    <title>Vue App</title>
  </head>

  <body>
    <div id="app">{{message}}</div>

    <script>
      const App = new Vue({
        el: '#app',
        data: {
          message: 'Hello Vue!',
        },
      })
    </script>
  </body>
</html>
```

Ok, this is not very impressive, but  the important point is that Vue is just JavaScript.

### Vue CLI

More often, you won't be injecting Vue into a static HTML file, but you'll be taking advantage of the Node ecosystem. The easiest way we can do this is   [Vue CLI](https://cli.vuejs.org/), or the Vue Command Line Interface. As mentioned in the prerequisites, you should be familiar with npm and how to work with local and global packages.

First, we'll install Vue CLI.

in your terminal:
```shell
# install with npm
npm i -g @vue/cli @vue/cli-service-global
```

Now that we have Vue CLI installed globally, we can use the  `vue`  command anywhere. We'll use  [vue create](https://cli.vuejs.org/guide/creating-a-project.html#vue-create)  to start a new project.

> `vue create`  is the equivalent to  `create-react-app`.

```shell
vue create vue-app
```

You'll be given an option to do default or manual, and we can just select default.

```
terminal

Vue CLI v3.7.0
? Please pick a preset: (Use arrow keys)
❯ default (babel, eslint)
  Manually select features
```

Once that's done, you can move to the new app that's been created and  `serve`  to run the dev server.

```
shell

cd vue-app
npm run serve
# or
yarn serve
```

Once that's done, you can navigate to  `http://localhost:8080/`  to see the default page.

### Ready, set go!
At this point, you're all set up and ready to go with Vue. 

### Vue DevTools

One final thing to have in your toolbelt while working with Vue is Vue DevTools. It's an add-on to regular DeveloperTools which will show you all the information about your components - their state, methods, etc.

 [Vue DevTools on Chrome](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?hl=en)



## Getting Started

Yes, you're all set up! You have a new Vue boilerplate app. In the project files, you have a  `public`  folder which contains  `index.html`, and an  `src`  folder with  `main.js`  as the entry point. We're introduced to  `.vue`  files, with the  `HelloWorld.vue`  and  `App.vue`  components.

### Entry point

In  `main.js`, we're bringing in  `Vue`  and rendering the App to our app div in  `index.html`. This file won't need to change.

**src/main.js**

```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  render: (h) => h(App),
}).$mount('#app')
```

## Anatomy of a Vue file

Anything else we make will be a  `.vue`  file, which always consists of three things:

-   `<template>`
-   `<script>`
-   `<style>`


This may seem strange to you, as it did to me at first. I originally learned front end coding with a focus on separation of concerns for HTML, CSS, and JavaScript, and here we have all three together. Yet JavaScript and the way we design apps has evolved, and keeping our styles and view and component coupled together is generally considered an advantage and improves maintainability.

The data and logic for the component goes in the  `<script>`  tag, but only  `name`  is required. The  `<style>`  tag is just CSS. 

### Now let's start actually building our teacher app.

This tutorial is about functionality, not styles, but instead of working with Bootstrap let's try a new CSS framework out. Today we'll work with Primitive UI, A lightweight framework. 

Now we're going to link to  [Primitive UI](https://github.com/taniarascia/primitive)  in the  `index.html`  file to add some easy default styles.

```html
<link rel="stylesheet" href="https://unpkg.com/primitive-ui/dist/css/main.css" />
```

## Creating a Component

Create a file called  `teachersTable.vue`  in  `src/components`. We're going to create a simple HTML table with some data.

src/components/teachersTable.vue

```html
<template>
  <div id="teacher-table">
    <table>
      <thead>
        <tr>
          <th>Teacher name</th>
          <th>Teacher email</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Koen Eelen</td>
          <td>Koen@becode.org</td>
        </tr>
        <tr>
          <td>Tim Broos</td>
          <td>tim@becode.org</td>
        </tr>
        <tr>
          <td>Sicco Smit</td>
          <td>sicco@becode.org</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  export default {
    name: 'teacher-table',
  }
</script>

<style scoped></style>
```


We're exporting  `teacherTable`  and importing it into  `App.vue`. In our  `import`, we can use  `@`  to reference the  `src`  folder.  `App.vue`  knows which components it can use via the  `components`  property. All imported components must be added there. I've also added in some global styles.

src/App.vue

```html
<template>
  <div id="app" class="small-container">
    <h1>Becode Teachers</h1>

    <teacher-table />
  </div>
</template>

<script>
  import teacherTable from '@/components/BecodeTeachersTable.vue'

  export default {
    name: 'app',
    components: {
      teacherTable,
    },
  }
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>
```


We want to refactor this already to use data in the form of arrays and object as opposed to hard coding all our values into the table. So let's add a  `data()`  method, and return a  `teachers`  array. We're also going to add IDs to each one to identify each teacher.

App.vue

```js
import teacherTable from '@/components/teacherTable.vue'

export default {
  name: 'app',
  components: {
    teacherTable,
  },
  data() {
    return {
      teachers: [
        {
          id: 1,
          name: 'Koen Eelen,',
          email: 'koen@becode.org',
        },
        {
          id: 2,
          name: 'Tim Broos',
          email: 'tim@becode.org',
        },
        {
          id: 3,
          name: 'Sicco Smit',
          email: 'sicco@becode.org',
        },
      ],
    }
  },
}
```


Now we have to pass this data to  `teacherTable`. We can do that by passing the data down as a property. An attribute that begins with a colon  `:`  will allow you to pass data. The more verbose version would be  `v-bind`. In this case we'll pass our  `teachers`  array.

```html
<teacher-table :teachers="teachers" />

<!-- this is the same thing -->
<teacher-table v-bind:teacher="teachers" />
```

Now on the  `teacherTable`  side, we want to retrieve that data, so we tell the component that it will receive props, in this case an  `Array`.

TeacherTable.vue

```js
export default {
  name: 'teacher-table',
  props: {
    teacher: Array,
  },
}
```

### Loops

Now that we have the data, we want to loop through the data and display the DOM nodes accordingly. We'll do this with the  `v-for`  attribute. Now that we can retrieve  `teacher`  in  `teacherTable`, we'll display one table row per teacher.

teacherTable.vue

```html
<template>
  <div id="teacher-table">
    <table>
      <!-- ...thead... -->
      <tbody>
        <tr v-for="teacher in teachers" :key="teacher.id">
          <td>{{ teacher.name }}</td>
          <td>{{ teacher.email }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
```

Vue has a requirement for uniquely identifying any element in an array, so we'll use  `:key`  on the table row and set it to a unique value.

Now our table hasn't changed from a view perspective, but it is now set up to work with data more efficiently.


## Forms

Now we're successfully accomplishing the "Read" portion of a CRUD app, but the next  thing to do is add the ability to create a new teacher. We're going to create an add teacher form.

Make  `teacherForm.vue`  and set it up a field to enter name, email, and a button to submit. I'll go ahead and create a  `teacher`  data property with  `name`  and  `email`  on it.

src/components/teacherForm.vue

```html
<template>
  <div id="teacher-form">
    <form>
      <label>teacher name</label>
      <input type="text" />
      <label>teacher Email</label>
      <input type="text" />
      <button>Add teacher</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'teacher-form',
    data() {
      return {
        teacher: {
          name: '',
          email: '',
        },
      }
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>
```

We'll also need to add this to App.vue

src/components/App.vue

```html
<template>
  <div id="app" class="small-container">
    <h1>Teachers</h1>

    <teacher-form />
    <teacher-table :teachers="teachers" />
  </div>
</template>

<script>
  import teacherTable from '@/components/teacherTable.vue'
  import teacherForm from '@/components/teacherForm.vue'

  export default {
    name: 'app',
    components: {
      teacherTable,
      teacherForm,
    },
    data: {
      // ...
    },
  }
</script>
``

Now we have to figure out how to get the data that we're writing in the input into Vue's component state. To do that we'll use  `v-model`.  [v-model](https://vuejs.org/v2/guide/forms.html)  is some built-in Vue syntactic sugar for updating an input value with an onchange event.

teacherForm.vue

```html
<template>
  <div id="teacher-form">
    <form>
      <label>teacher name</label>
      <input v-model="teacher.name" type="text" />
      <label>teacher Email</label>
      <input v-model="teacher.email" type="text" />
      <button>Add teacher</button>
    </form>
  </div>
</template>
```

Now that you've added this, you can see in Vue DevTools that the state of the component changes. We just need to submit these values and update the parent (App) state with the new teacher object.

### Event listeners

We want to do an  `onsubmit`  event on the form. We can do that with  `v-on:submit`, or  `@submit`  for short. This convention will be the same for  `@click`/`v-on:click`  or any other similar event. The  `submit`  event also has a handy  `prevent`  we can add to it, which is the same as putting  `event.preventDefault()`  inside the submit function, since we won't be using the default GET/POST methods provided by forms.

Let's add this to the form, and reference a  `handleSubmit`  method we'll make.

teacherForm.vue

```html
<form @submit.prevent="handleSubmit"></form>
```

### Methods

Now we're going to create our first method on a component. Below  `data()`, we can create a  `methods`  object, which will contain all the custom methods we create. Let's add  `handleSubmit`  there.

teacherForm.vue

```js
export default {
  name: 'teacher-form',
  data() {
    return {
      teacher: {
        name: '',
        email: '',
      },
    }
  },
  methods: {
    handleSubmit() {
      console.log('testing handleSubmit')
    },
  },
}
```

### Emitting events to the parent

Now if you try to submit the form, you'll see the message logged in the console. We know the form submit method is working properly, so we can pass the data up to  `App`  now. We'll do this using  `$emit`.

Emit broadcasts a name of an event and data to its parent component, like so.

```js
this.$emit('name-of-emitted-event', dataToPass)
```

In our case, we'll create an event called  `add:teacher`, and pass  `this.teacher`.

teacherform.vue

```js
handleSubmit() {
  this.$emit('add:teacher, this.teacher)
}
```

> The  `add:teacher`  syntax (as opposed to  `add-teacher`  or something else) is recommended in  [the Vue documentation](https://vuejs.org/v2/guide/components-custom-events.html#sync-Modifier)

Once you add this, click to add form button and go to Vue DevTools. You'll see a notification for a new event, and it will tell you the name, source, and payload, which in this case is an object we created.



### Retrieving events from the child

Now  `teacher-form`  is broadcasting its emitted event, but we need to capture the event and value in the parent to work with it.

The first thing we need to do is make  `teacher-form`  acknowledge and handle the emitted event, and invoke a new method. It will look like this:

```html
<component @name-of-emitted-event="methodToCallOnceEmitted"></component>
```

So let's add that to  `App.vue`.

App.vue

```html
<teacher-form @add:teacher="addTeacher" />
```

Now we just have to create the  `addTeacher`  method on  `App.vue`, which will modify the teacher array by adding a new item to it. That will essentially look like this:

App.vue

```js
methods: {
  addTeacher(teacher) {
    this.teachers = [...this.teachers, teacher]
  }
}
```

Since I have to make an  `id`  as well, I'll just write some code to get the new teachers ID based on number of items in the array. 

```js
addTeacher(teacher) {
  const lastId =
    this.teachers.length > 0
      ? this.teachers[this.teachers.length - 1].id
      : 0;
  const id = lastId + 1;
  const newTeacher = { ...teacher, id };

  this.teachers = [...this.teachers, newTeacher];
}
```

Now with this, you can add new teachers. Note that the new teacher will not persist, as it is front end only and not connected to a database.


## Basic form validation

This works, but we can clean it up a little. We want to...

-   Show a success message if everything went through
-   Show an error message if something was missing
-   Highlight the inputs that have invalid data
-   Clear the inputs after the form is done submitting properly, and
-   Focus on the first item in the input after successful submission

### Computed properties

In Vue, we can use computed properties, which are functions that are automatically computed when something changes. This way we can avoid putting complex logic in the Vue template itself. I'm just going to put a basic check to make sure the field isn't empty for both fields.

TeacherForm.vue

```js
computed: {
  invalidName() {
    return this.teacher.name === ''
  },

  invalidEmail() {
    return this.teacher.email === ''
  },
},
```

To set all this up, I'm going to add a  `submitting`  state, to check whether or not the form is currently being submitted, an  `error`  state if something went wrong, and a  `success`  state if it went through properly.

TeacherForm.vue

```js
data() {
  return {
    submitting: false,
    error: false,
    success: false,
    teacher: {
      name: '',
      email: '',
    }
  }
}
```

The submit function will first clear whether or not  `success`  or  `error`  have been set, the start submitting. It'll check our computed properties, and if either is true, an  `error`  will be set. If not, we can submit, and set all the states back to default.

TeacherForm.vue

```js
methods: {
  handleSubmit() {
    this.submitting = true
    this.clearStatus()

    if (this.invalidName || this.invalidEmail) {
      this.error = true
      return
    }

    this.$emit('add:teacher', this.teacher)
    this.teacher = {
      name: '',
      email: '',
    }
    this.error = false
    this.success = true
    this.submitting = false
  },

  clearStatus() {
    this.success = false
    this.error = false
  }
}
```

Since we want an error message and a success message, I'll set up the CSS for that.

TeacherForm.vue

```html
<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>
```

Finally, we'll set up the form. If the form is submitting and one of the computed properties is invalid, we want to set a  `has-error`  class on the input. Using  `:class=`  ensures that the class will be treated as JavaScript instead of a plain string. We can make sure the statuses get cleared on focus and keypress events, and we have success and error messages displayed accordingly at the bottom.

TeacherForm.vue

```html
<form @submit.prevent="handleSubmit">
  <label>Teacher name</label>
  <input
    type="text"
    :class="{ 'has-error': submitting && invalidName }"
    v-model="teacher.name"
    @focus="clearStatus"
    @keypress="clearStatus"
  />
  <label>teacher Email</label>
  <input
    type="text"
    :class="{ 'has-error': submitting && invalidEmail }"
    v-model="teacher.email"
    @focus="clearStatus"
  />
  <p v-if="error && submitting" class="error-message">
    ❗Please fill out all required fields
  </p>
  <p v-if="success" class="success-message">✅ Teacher successfully added</p>
  <button>Add teacher</button>
</form>
```

### Conditonals

You'll notice a  `v-if`  property. This is a conditional in vue. In this case, the  `<p>`  element will only be displayed if the condition is true.

There is also a  `v-else-if`, and  `v-else`  property, which work the same as their vanilla JS counterparts.

Now that that's complete, we can see these conditionally rendered elements. Here's the error message on a missing field.

And here's the success message. Hooray!


### Adding a reference

There's one more small improvement we can make. After submitting the form, it would be nice if the focus went back on the first item to make it easy to add many items without clicking around. We can do that with  refs, which we can use to target a specific element.

We can just add a ref to the first input...

TeacherForm.vue

```html
<input ref="first" ... />
```

And  `focus`  that ref after submitting the form in  `handleSubmit`.

TeacherForm.vue

```js
this.$emit('add:teacher', this.teacher)
this.$refs.first.focus()
```

Now after you submit the focus will automatically go to the first field in the form. The  `@keypress`  event to  `clearStatus`  we added to it before will ensure the success or error message goes away once you start typing.


## Deleting Items

Now that the form is done, we have to finish the other actions on the table - editing and deleting. We'll start with deleting, which is an easier operation.

First, we'll update the table to have an "Actions" row, and add buttons for editing and deleting.

TeacherTable.vue

```html
<template>
  <div id="teacher-table">
    <table>
      <thead>
        <tr>
          <th>Teacher name</th>
          <th>Teacher email</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="teacher in teachers" :key="teacher.id">
          <td>{{ teacher.name }}</td>
          <td>{{ teacher.email }}</td>
          <td>
            <button>Edit</button>
            <button>Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
  button {
    margin: 0 0.5rem 0 0;
  }
</style>
```

We'll emit an event like before, this time called  `deleteTeacher`. We can pass the  `id`  of the teacher as the payload.

TeacherTable.vue

```html
<button @click="$emit('delete:teacher', teacher.id)">Delete</button>
```

Back in  `App.vue`, we have to tell  `teacher-table`  to perform an action on  `delete-teacher`...

App.vue

```html
<teacher-table :teacher="teachers" @delete:teacher="deleteTeacher" />
```

And we'll filter the deleted row out.

App.vue

```js
methods: {
  addTeacher(teacher) {...},
  deleteTeacher(id) {
    this.teachers = this.teachers.filter(
      teacher => teacher.id !== id
    )
  }
}
```

Now you'll notice you can delete items. Let's just add a message in case there are no teachers.

TeacherTable.vue

```html
<div id="teacher-table">
  <p v-if="teachers.length < 1" class="empty-table">No teachers</p>
  <table v-else>
    ...
  </table>
</div>
```

We can successfully add and delete teachers now.



### Editing Items

Editing is a little more complex than deleting. The setup from  `App.vue`  is simple though, so we'll do that first. Just add the  `edit:teacher`  event that we'll be making:

App.vue

```html
<teacher-table
  :teachers="teachers"
  @delete:teacher="deleteTeacher"
  @edit:teacher="editTeacher"
/>
```

And create the  `editTeacher`  method, which will take  `id`  and  `updatedTeacher`  parameters, map through the  `teachers`  array, and update the correct teacher.

App.vue

```js
editTeacher(id, updatedTeacher) {
  this.teachers = this.teachers.map(teacher =>
    teacher.id === id ? updatedTeacher : teacher
  )
}
```

Simple enough.

Now back in  `TeacherTable.vue`, we'll basically want to make an "edit mode" that is enabled when the button is pressed.

TeacherTable.vue

```html
<button @click="editMode(teacher.id)">Edit</button>
```

We'll create an  `editing`  state that will get set to the  `id`  of the row that's currently being edited when  `editMode`  is enabled.  `TeacherTable`  will have it's own local  `editTeacher`  method, which emits  `edit:teacher`  to  `App`  if the fields aren't empty, and resets the  `editing`  state.

TeacherTable.vue

```js
data() {
  return {
    editing: null,
  }
},
methods: {
  editMode(id) {
    this.editing = id
  },

  editTeacher(teacher) {
    if (teacher.name === '' || teacher.email === '') return
    this.$emit('edit:teacher', teacher.id, teacher)
    this.editing = null
  }
}
```

Here's the current state of our table row - we're just displaying the values.

```html
<tr v-for="teacher in teachers" :key="teacher.id">
  <td>{{ teacher.name }}</td>
  <td>{{ teacher.email }}</td>
  <td>
    <button @click="editMode(teacher.id)">Edit</button>
    <button @click="$emit('delete:teacher', teacher.id)">Delete</button>
  </td>
</tr>
```

To make it editable, we'll check if  `editing === teacher.id`  is true for a particular row, and display and input instead. We'll also add a cancel button that will cancel the editing by setting it to null.

```html
<tr v-for="teacher in teachers" :key="teacher.id">
  <td v-if="editing === teacher.id">
    <input type="text" v-model="teacher.name" />
  </td>
  <td v-else>{{teacher.name}}</td>
  <td v-if="editing === teacher.id">
    <input type="text" v-model="teacher.email" />
  </td>
  <td v-else>{{teacher.email}}</td>
  <td v-if="editing === teacher.id">
    <button @click="editteacher(teacher)">Save</button>
    <button class="muted-button" @click="editing = null">Cancel</button>
  </td>
  <td v-else>
    <button @click="editMode(teacher.id)">Edit</button>
    <button @click="$emit('delete:teacher', teacher.id)">Delete</button>
  </td>
</tr>
```

And now I can edit a single row at a time!



Editing works, but you still can't cancel the state from updating with this code, even if the new values don't get sent to the API call. We'll create  `cancelEdit`, and make the cancel button call  `@click="cancelEdit(teacher)"`  and remove  `.id`  from the edit button. We'll make a cached teacher that we can return to.

```js
editMode(teacher) {
  this.cachedTeacher = Object.assign({}, teacher)
  this.editing = teacher.id
},
cancelEdit(teacher) {
  Object.assign(teacher, this.cachedTeacher)
  this.editing = null;
}
```

At this point, the app is technically complete, but a real production app will probably be making API calls to a back end database, so we'll make a mock version of that.



## Making Asynchronous REST API Calls

We're going to use  [JSON Placeholder](https://jsonplaceholder.typicode.com/)  to make fake API calls that will give us real responses. We can  `GET`  values (for example, visit  [https://jsonplaceholder.typicode.com/users](https://jsonplaceholder.typicode.com/users)  to see the  `users`  JSON we'll be using), and we can make  `POST`,  `PUT`, and  `DELETE`  requests. These requests will not persist in a real database because they're for example purposes.

An asynchronous method with  [async/await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)  will look something like this, using a  [try/catch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/try...catch)  block.

```js
async asynchronousMethod() {
  try {
    const response = await fetch('url')
    const data = await response.json()

    // do something with `data`
  } catch (error) {
    // do something with `error`
  }
}
```

So at this point, I'll replace all our CRUD methods with  `async`  methods, and update the data via the API as well as the front end.

### Lifecycle methods

With GET, we'll want to remove all the pre-populated data we have in the  `teacher`  array, and replace it with the data from the API. We'll call that  `GET`  in the  `mounted`  [lifecycle method](https://vuejs.org/v2/guide/instance.html#Lifecycle-Diagram).

[`mounted`](https://vuejs.org/v2/api/#mounted)  tells our component to perform the action once the component is actually inserted to the DOM. This is a common way to display data from an API. (Some use the  `created`  lifecycle for this task.)

App.vue

```js
export default {
  name: 'app',
  components: {
    TeacherTable,
    TeacherForm,
  },
  data() {
    return {
      teachers: [],
    }
  },

  mounted() {
    this.getTeacher()
  },
}
```

So now we can update all our CRUD methods with their asynchronous API-call equivalents.

### GET

Retrieve a resource.

App.vue

```js
async getTeachers() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users')
    const data = await response.json()
    this.teachers = data
  } catch (error) {
    console.error(error)
  }
}
```

### POST

Create a new resource (non-idempotent).

App.vue

```js
async addTeacher(teacher) {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users', {
      method: 'POST',
      body: JSON.stringify(teacher),
      headers: { 'Content-type': 'application/json; charset=UTF-8' },
    })
    const data = await response.json()
    this.teachers = [...this.teachers, data]
  } catch (error) {
    console.error(error)
  }
}
```

### PUT

Update an existing resource.

App.vue

```js
async editTeacher(id, updatedTeacher) {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
      method: 'PUT',
      body: JSON.stringify(updatedTeacher),
      headers: { 'Content-type': 'application/json; charset=UTF-8' },
    })
    const data = await response.json()
    this.teachers = this.teachers.map(teacher => (teacher.id === id ? data : teacher))
  } catch (error) {
    console.error(error)
  }
}
```

### DELETE

Remove an existing resource.

App.vue

```js
async deleteTeacher(id) {
  try {
    await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
      method: "DELETE"
    });
    this.teachers = this.teachers.filter(teacher => teacher.id !== id);
  } catch (error) {
    console.error(error);
  }
}
```

Ok, all API calls should be working properly, and we're getting data from JSON Placeholder instead of our own, static data.

Congrats! Your app is complete!
