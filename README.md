053 Handling Exceptions
=======================

Followed along with Railscast 053 Handling Exceptions

[Blog Post](http://patrickperey.com/railscast-053-handling-exceptions) @ [PatrickPerey.com](http://patrickperey.com)

```ruby
class Forbidden < StandardError; end
...
def show
  raise Forbidden, 'You are not allowed to access this product.'
end
```

```ruby
config.exceptions_app = self.routes
```

``` ruby
match '(errors)/:status', to: 'errors#show', constraints: {status: /\d{3}/}, via: :get
```

```ruby
class ErrorsController < ApplicationController
  def show
    @exception = env["action_dispatch.exception"]
    respond_to do |format|
      format.html { render action: request.path[1..-1] }
      format.html { render json: {status: request.path[1..-1], error: @exception.message} }
    end
  end
end
```
