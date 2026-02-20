
# CKEditor 4.13.1 Integration in Rails

This repository demonstrates how to integrate **CKEditor 4.13.1** into a Ruby on Rails application with toolbar customization and emoji support.

---

## Installation Steps

### 1. Add Required Gems

Add the following gems to your `Gemfile`:

```ruby
gem 'jquery-rails'
gem 'ckeditor', '~> 4.2'
```

Then run:

```bash
bundle install
```

---

### 2. Configure CKEditor CDN

Create a file:

```
config/initializers/ckeditor.rb
```

Add:

```ruby
Ckeditor.setup do |config|
  # //cdn.ckeditor.com/<version.number>/ckeditor.js
  config.cdn_url = "//cdn.ckeditor.com/4.6.1/basic/ckeditor.js"
end
```

---

### 3. Include CKEditor in Layout

In:

```
app/views/layouts/application.html.erb
```

Add:

```erb
<%= javascript_include_tag Ckeditor.cdn_url %>
```

---

### 4. Precompile CKEditor Assets

In:

```
config/initializers/assets.rb
```

Add:

```ruby
Rails.application.config.assets.precompile += %w[ckeditor/config.js]
```

---

### 5. Use CKEditor in Forms

```erb
<%= form.cktext_area :content, value: 'Default value', id: 'sometext' %>
```

---

## Toolbar Customization

Create:

```
app/assets/javascripts/ckeditor/config.js
```

Add:

```javascript
CKEDITOR.editorConfig = function (config) {

  config.toolbar_mini = [
    ["Bold", "Italic", "Underline", "Strike", "-", "Subscript", "Superscript"]
  ];

  config.toolbar = "mini";
};
```

This file allows you to customize the CKEditor toolbar.

---

## Enable Emoji Support

In:

```
app/assets/javascripts/application.js
```

Add the following line **before**:

```javascript
//= require_tree .
```

Add:

```javascript
//= require ckeditor/init
```

Update your form as:

```erb
<%= form.cktext_area :content,
      value: 'Default value',
      id: 'sometext',
      ckeditor: { toolbar: 'Full' } %>
```

---

## Custom CKEditor Build (Optional)

1. Visit: https://ckeditor.com/ckeditor-4/download/
2. Use the **Online Builder** to customize CKEditor.
3. Download and extract the package.
4. Open:

```
/ckeditor/samples/index.html
```

Copy required folders like:

```
lang
skins
plugins
```

From:

```
ckeditor_4.13.1/ckeditor/
```

To:

```
app/assets/javascripts/ckeditor/
```

---

## Run the Server

```bash
rails server
```

Open your form page to see CKEditor in action.

---

## Author

Pawan Bharti
