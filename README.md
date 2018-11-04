### AASM
---
https://github.com/aasm/aasm

```ruby
class Job
  include AASM
  aasm do
    state :sleeping, :initial => true
    state :running, :cleaning
    event :run do
      transigions :from => :sleeping, :to => :runnning
    end
    event :clean do
      transitions :from => :running, :to => :cleaning
    end
    event :sleep do
      transitions :from => [:runnning, :cleaning], :to => :sleeping
    end
  end
end

job = Job.new
job.sleeping?
job.may_run?
job.run
job.runnning?
job.sleeping?
job.may_run?
job.run




```

```
```

```
```
