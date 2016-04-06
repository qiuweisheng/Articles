ActiveSupport::Callbacks介绍
======
ActiveSupport::Callbacks是一个Ruby模块，可以让包含它的类方便地定义、设置以及运行回调。以下是一个例子：
```ruby
require 'active_support/callbacks'

class Record
  include ActiveSupport::Callbacks
  
  define_callbacks :save
  set_callback :save, :before, :saving_message
  set_callback :save, :after do |object|
    puts 'saved'
  end
  set_callback :save, :around, :around_save
  
  def saving_message
    puts 'saving...'
  end
  
  def around_save
    puts 'before save'
    yield
    puts 'after save'
  end
  
  def save
    run_callbacks :save do
      puts '- save'
    end
  end
end

record = Record.new
record.save
```