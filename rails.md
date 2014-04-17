Use `find_each` instead of `each` on ActiveRecord relations

```ruby
# bad
# very inefficient since it will try to instantiate all the objects at once
Person.all.each do |person|
  person.do_awesome_stuff
end

# good
# http://api.rubyonrails.org/classes/ActiveRecord/Batches.html#method-i-find_each
Person.find_each do |person|
  person.do_awesome_stuff
end
```

Avoid duplicated work by future calls with memoization.<br>
http://gavinmiller.io/2013/basics-of-ruby-memoization/<br>
http://gavinmiller.io/2013/advanced-memoization-in-ruby/

```ruby
# https://github.com/bydmm/careereagle/commit/a250bf5a6bf52144af9401af3c8a2f7613adf63c
# bad
def current_user
  User.find(session[:user_id])
end

# good
def current_user
  @current_user ||= User.find(session[:user_id])
end
```

Use `present?`, `empty?` and `blank?` on ActiveRecord relations

```ruby
class User < ActiveRecord::Base
  has_many :licenses
end

user = User.find(1)

# bad
user.licenses.count > 0
user.licenses.count == 0

# good
user.licenses.present?
user.licenses.empty?
```

Do not prefix method name with is, get or set.

```ruby
# bad
class Video
  def is_available?; end
  def get_video_picture; end
  def set_video_picture(pic); end
end

# good
class Video
  def available?; end
  def video_picture; end
  def video_picture=(pic); end
end
```
