# Writing a Rails Engine
## Erik Michael-Ober [@sferik](https://twitter.com/sferik)

http://www.confreaks.com/videos/1109-gogaruco2012-writing-a-rails-engine

### Introduction
All a rails app is a bootable rails engine  
Engines do not know how to start themselves, but are everything else, MVC  
Engines can plugin to engines  

Rails engines are fundamental building block of rails

### History
James Adam is creator of rails engines  
1st commit to engines plugin was 10/31/2005  
Rails 0.14.2  
Really old concept/feature  

DHH was against engines!

James Adam thought it would be "Madness" to have engines in rails
  
Merb slices introduced on 05/21/2008
Slice out bits of functionality and use across multiple applications

Rails and Merb merge on 12/23/2008  
Concepts of merb, including engines, were built into rails core

The Russian Doll Pattern by Carl Lerche and Yehuda Katz  
Apps within apps

Ruby Summer of Code 2010  
Piotr Sarnacki used Russian Doll Pattern and implemented it in rails  
Mentored by Carl, Yehuda and Jose Valim 

Bogdan Gaza rebuilt MerbAdmin

Rails 3.0 uses engines!  
Pain point was assets which had to be copied via rake task or generator

Rails 3.1 Asset Pipeline, FTW  
Puts every engine in load path for assets  
Looks in all engines to load assets  
Engines became first class citizens!

Rails 3.2 deprecates vendor/plugins  
The way forward is engines  
Rails 4, engines are the only way

### Write a Rails engine

Easy, same as writing a rails app  
`$ rails plugin new my_engine --mountable`  
very similar file system  

 * Engines are namespaced by modules
 * Engines inherit from Rails::Engine which adds engine to load path
 * Engine is not added to Gemfile, specify via gemspec
 * Can have custom rake tasks in lib/tasks and scoped to engine name
 * Can define generators lib/generators and scoped by engine name
 * Can write migrations db/migrations and scoped by engine name
  * `rake my_engine::install::migrations` only copy in new migrations
 * Routes are defined in engine and engine is mounted in client app
   routes at a certain path

### Testing a Rails engine

Best practice is 
 1. to create a dummy app in test directory
 2. mount engine in dummy app
 3. test the dummy app

For more info: http://guides.rubyonrails.org/engines.html

### When should I write an engine?

1. If you are at a point and you have two apps which need to share logic,
slice out the logic into a gem to be shared.
2. A base like scaffolding, assets or template which can be mounted
into multiple apps and reused

