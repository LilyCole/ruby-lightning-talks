# Formtastic

Formtastic is a Rails FormBuilder DSL (with some other goodies) to make it far easier to create beautiful, semantically rich, syntactically awesome, readily stylable and wonderfully accessible HTML forms in your Rails applications.

## Whats So Great About Formtastic

* Creating complex forms with little code
* Can handle has_many/belongs_to associations

## Gem Demo (Gemo?)

* RailsCast "https://www.youtube.com/watch?v=kPOn4xXxF5s"

## Examples

Easy Simple Forms

I created the following model:

```Ruby
  create_table "heroines", force: :cascade do |t|
    t.string   "name"
    t.string   "gender"
    t.date     "birthdate"
    t.boolean  "active"
    t.integer  "likability"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end
```
    
I also constrained the attribute "likability" in the following ways in the model:

```Ruby
class Heroine < ApplicationRecord
    validates_numericality_of :likability, 
    :less_than_or_equal_to => 10, 
    :greater_than_or_equal_to => 0, 
    :only_integer => true
end
```

By using formtastic, I made this readble semantic form with the following options:

```Ruby
<%= semantic_form_for @heroine do |f| %>
  <%= f.inputs do %>
    <%= f.input :name %>
    <%= f.input :gender, :as => :radio, :collection => ["Male", "Female", "Other"]%>
    <%= f.input :birthdate, :start_year => 1920 %>
    <%= f.input :active %>
    <%= f.input :likability, :as => :range %>
  <% end %>
  <%= f.actions %>
<% end %>
```

See the form here:

<img src="http://i.imgur.com/U7HJjap.png" height="300px">

**Note that:**
- Gender (string) is presented as a Radio Button with only three input options
- Birthdate (date) is presented as a Date object, allowing years from 1920 to present
- Active (boolean) is presented as a checkbox
- Likability is presented as a slider range

## Setup

1 - Add to your **Gemfile**: ```gem 'formtastic', '~> 3.0'```

2 - Rebundle: ```> bundle```

3 - Run installation generator: ```> rails generate formtastic:install```

4 - Add to **app/assets/stylesheets/application.css**:
```
 *= require formtastic
 *= require my_formtastic_changes
```

5 - In **views/layouts/application.html.erb**: 

```<%= stylesheet_link_tag 'application', 'formtastic', 'my_formtastic_changes' %>```

6 - In **config/initializers/assets.rb**:
```
Rails.application.config.assets.precompile += %w( formtastic.css )
Rails.application.config.assets.precompile += %w( my_formtastic_changes.css )
```

7 - Start or restart your server after changing assets.rb file

## Resources

<li> [Github and Docs](https://github.com/justinfrench/formtastic)
