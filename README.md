## Bootstrap

If you remember from class today I had some issues with the navbar. It seems that it's an issue with the jQuery library and its latest version. It doesn't work [correctly with Bootstrap](https://github.com/twbs/bootstrap/issues/30553).

Here's the fix. I've also included an updated way to install Bootstrap as I think the way I showed you today isn't best practice.

Also take a look at the code in `index.html.erb` if you want to see how you can you `row` and `col`.

1. Create your project
2. Run this command:

    ```
    yarn add bootstrap jquery@3.4.1 popper.js
    ```

3. This time we're installing a version of jquery that works with bootstrap, this might be patched in the coming days
4. You `app/javascript/packs/applications.js` file should look like this:

    ```js
    require("@rails/ujs").start()
    require("turbolinks").start()
    require("@rails/activestorage").start()
    require("channels")

    import "bootstrap"
    import "../stylesheets/application"
    ```

5. Your `config/webpack/environment.js` file should look like this:

    ```js
    const { environment } = require('@rails/webpacker')

    const webpack = require('webpack')

    environment.plugins.append("Provide", new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery',
      Popper: ['popper.js', 'default']
    }))

    module.exports = environment
    ```

6. Create a new directory called `stylesheets` in your `javascript` directory:
7. Create a new file in the stylesheets directory called application.scss, your `app/javascript/stylesheets/application.scss` file should look like this:

    ```scss
    @import "~bootstrap/scss/bootstrap";
    ```

8. Your `app/views/layouts/application.html.erb` file should look like this:

    ```
    <!DOCTYPE html>
    <html>
      <head>
        <title>BootstrapTest</title>
        <%= csrf_meta_tags %>
        <%= csp_meta_tag %>
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>
        <%= stylesheet_pack_tag 'application' %>
        <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
      </head>

      <body>
        <%= yield %>
      </body>
    </html>
    ```

9. Try out some bootstrap like adding in a navbar, try to override it in your `main.scss` file, have fun 💅
10. I follow the same approach as [what this guy did](https://gorails.com/episodes/how-to-use-bootstrap-with-webpack-and-rails)