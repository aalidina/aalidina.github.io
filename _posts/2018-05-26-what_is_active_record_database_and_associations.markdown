---
layout: post
title:      "What is Active Record Database and Associations"
date:       2018-05-26 18:37:41 +0000
permalink:  what_is_active_record_database_and_associations
---


 Active Record is the M in MVC - the model - which is the layer of the system responsible for representing business data and logic. It's a object rational mapping (ORM) allows you to connect your application to the database and eliminates the need to use the SQL queries within the application.
 
 In order for active record to work you have to setup the tables in the db directory under the migration file and run rake db:migrations in order to create the table. This will create a schema file by examining the database. They are not designed to be edited they just represent the current state of the database. Schema files are also useful if you want a quick look at what attributes an Active Record object has. This information is not in the model's code and is frequently spread across several migrations, but the information is nicely summed up in the schema file. Once that is done you have to setup the relations in the model file in order for the database to work. 
 
 Example of activerecord Schema file
 
 ActiveRecord::Schema.define do
  create_table :authors do |t|
    t.string :name, null: false
  end

  add_index :authors, :name, :unique

  create_table :posts do |t|
    t.integer :author_id, null: false
    t.string :subject
    t.text :body
    t.boolean :private, default: false
  end

  add_index :posts, :author_id
end
 
When naming the model files the name has to be singular and the controller name needs to be pluralized. Although these mappings can be defined explicitly, it's recommended to follow naming conventions, especially when getting started with the library. Active Records also provides associations so we can streamline operations by declaratively telling Rails that there is a connection between the models. There are six types of associations provided by active record that you can read more on [Active Record Associations](http://guides.rubyonrails.org/association_basics.html)
 
 [What does schema.rb do?](https://stackoverflow.com/questions/9884429/rails-what-does-schema-rb-do)
 [APIdock](https://apidock.com/rails/ActiveRecord/Schema)

