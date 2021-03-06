# Rails example app with dry-system


> Object dependency management system based on dry-container and dry-auto_inject allowing you to configure reusable components in any environment, set up their load-paths, require needed files and instantiate objects automatically with the ability to have them injected as dependencies.

[dry container](https://dry-rb.org/gems/dry-system/master/container/)

## IoC container and autoload

File `config/initializers/app_container.rb` [link](/config/initializers/app_container.rb)

contains the main configuration and injector

```ruby
class AppContainer < Dry::System::Container
  configure do |config|
    config.name = :dry_rails_example
    config.root = Pathname('app')
    config.component_dirs.add 'services'
  end
end

AppImport = AppContainer.injector

AppContainer.finalize! if Rails.env.production?
```

## Tests

Contains stub for IoC containers

`spec/support/dry_system.rb` [link](/spec/support/dry_system.rb)

In tests container may be stubbed like this

```ruby
AppContainer.stub('container.name', -> { 'result' })
```
