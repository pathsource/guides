```rb
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
