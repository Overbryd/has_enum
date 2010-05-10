# has_enum

This is a plugin, to bring enumerations down to your models. It was written with simplicity in mind.

* Allow a set of options to be available
* Query records using named scopes
* Add your own validations
* Prefix query methods

The plugin comes in especially handy when dealing with processing states.

## Model

    class Model < ActiveRecord::Base
      has_enum :category, %w( stuff things misc ) , :query_methods => :in
      has_enum :color   , %w( red green blue )    , :query_methods => true, :validate => :presence, :named_scopes => true
      has_enum :size    , %w( small medium large ), :validate => false
      has_enum :foo     , %w( bar )               , :validate => lambda{ |model, attrib, value|
        model.errors.add(attrib, :unbar) unless value =~ /^bar/ }
    end

## Views

    radio_button_enum(object_name, method, options = {})
    
    select_enum(object_name, method, options = {})
