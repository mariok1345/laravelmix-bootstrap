/////////////////////////////////////////////////////////////////Laravel mix con Bootstrap////////////////////////////////////////


1. Creacion de las carpertas Resources y Public 
	Resources-------------> Sass
				js
	Public----------------> Css
				js
2.Correr el comando npm init -y

3.npm install laravel-mix --save -dev
4.cp -r node_modules/laravel-mix/setup/webpack.mix.js ./
5.integro el script en package.json

"scripts": { "dev": "npm run development", "development": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js", "watch": "npm run development -- --watch", "hot": "cross-env NODE_ENV=development node_modules/webpack-dev-server/bin/webpack-dev-server.js --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js", "prod": "npm run production", "production": "cross-env NODE_ENV=production node_modules/webpack/bin/webpack.js --no-progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js" }

6.integro la ruta en el que se procesaran y compilaran nuestro archivos

const mix = require('laravel-mix');

mix.js('resources/js/app.js', 'public/js')

.sass('resources/sass/style.scss', 'public/css');

6.npm install cross-env --save-dev 

integrar bootstrap

1.npm i bootstrap
2.npm i popper.js bootstrap
3.Crear archivo resources/js/bootstrap.js

pegar este bloque de codigo
'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
window._ = require('lodash');
import Popper from 'popper.js/dist/umd/popper.js';
/**
 * We'll load jQuery and the Bootstrap jQuery plugin which provides support
 * for JavaScript based Bootstrap features such as modals and tabs. This
 * code may be modified to fit the specific needs of your application.
 * Include the Popper.js library, since Boostrap 4 requires it
 */
try {
    window.$ = window.jQuery = require('jquery');
    window.Popper = Popper;
    require('bootstrap');
} catch (e) {
}

/**
 * Vue is a modern JavaScript library for building interactive web interfaces
 * using reactive data binding and reusable components. Vue's API is clean
 * and simple, leaving you to focus on building your next great project.
 */

window.Vue = require('vue');

/**
 * We'll load the axios HTTP library which allows us to easily issue requests
 * to our Laravel back-end. This library automatically handles sending the
 * CSRF token as a header based on the value of the "XSRF" token cookie.
 */

window.axios = require('axios');

window.axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';

/**
 * Next we will register the CSRF Token as a common header with Axios so that
 * all outgoing HTTP requests automatically have it attached. This is just
 * a simple convenience so we don't have to attach every token manually.
 */

let token = document.head.querySelector('meta[name="csrf-token"]');

if (token) {
    window.axios.defaults.headers.common['X-CSRF-TOKEN'] = token.content;
} else {
    console.error('CSRF token not found: https://laravel.com/docs/csrf#csrf-x-csrf-token');
}

/**
 * Echo exposes an expressive API for subscribing to channels and listening
 * for events that are broadcast by Laravel. Echo and event broadcasting
 * allows your team to easily build robust real-time web applications.
 */

// import Echo from 'laravel-echo'

// window.Pusher = require('pusher-js');

// window.Echo = new Echo({
//     broadcaster: 'pusher',
//     key: 'your-pusher-key'
// });

'''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
4.integrar en resources/sass/style.scss

@import "~bootstrap/scss/bootstrap";

5.npm run dev 