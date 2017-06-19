# Service Objects

### A. The problem identified

Service objects are a nice solution to use for controllers that have lots of complicated logic.  This can lead to long methods, and a controller object that has too many responsibilities.  Controller actions already have a lot of responsibility: they handle requests and responses.  Any other responsibility of a controller, ultimately belongs elsewhere.  

Take a look at the below code in a controller.  Not only is the code long, but it has nothing to do with handling a request or sending back a response.  Thus, it does not belong in our controller.

```ruby
require_relative 'setup'
require_relative 'exhaler'
require 'pry'

class DragonsController

  def has_run
    false
  end

  def exhale(dragon, rider, given_words)
    if !given_words.empty?
      dragon.say given_words
    elsif rider && rider.created_at <= (Time.now - 7*24*3600) && dragon.weight && dragon.weight >= 10000
      dragon.say 'We can crush anything!!'
    elsif
    # When rider is over a week old, then when dragon spits fire
    rider && rider.created_at <= (Time.now - 7*24*3600)
      dragon.say 'Eat Flames!!'
    else
      if rider && rider.created_at > (Time.now - 7*24*3600)
        dragon.say 'Bummer. No flames, just smoke.'
      end
    end
  end
end

```

### B. Solving long controller methods

To solve the problem of a bloated controller we employ a technique named replace method with a method object.  Take a look at the following resources to learn more:

* [Cleaner Controllers with Service Objects](https://blog.engineyard.com/2014/keeping-your-rails-controllers-dry-with-services)
* [Replace Method with method object](https://refactoring.com/catalog/replaceMethodWithMethodObject.html)
* [RailsConf Replace Method with Method Objects](https://www.youtube.com/watch?v=ozWzehOEeuI)
* [Replacing Methods with Method Objects Video] (https://www.youtube.com/watch?v=J4dlF0kcThQ)
<p class='util--hide'>View <a href='https://learn.co/lessons/service-objects-from-controllers'>Service Objects From Controllers</a> on Learn.co and start learning to code for free.</p>
