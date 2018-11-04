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

class Job
  aasm :whiny_transitions => false do
  end
end
job.running?
job.may_run?
job.run

class Job
  include AASM
  aasm do
    state :sleeping, :initial => true, :before_enter => :do_something
    state :running, before_enter: Proc.new { do_something && notify_somebody }
    state :finished
    after_all_transitions :log_status_change
    event :run, :after => :notify_somebody do
      before do
        log('Preparing to run')
      end
      transitions :from => :sleeping, :to => :running, :after => Proc.new {|*args| set_process(*args) }
      transitions :from => :running, :to => :finished, :after => LogRunTime
    end
    event :sleep do
      after do
      end
      error do |e|
      end
      transitions :from => :running, :to => :sleeping
    end
  end
  def log_status_change
    put "changing from #{assm.from_status} to #{aasm.to_state} {event: #{aasm.current_event}}"
  end
  def set_process(name)
  end
  def do_something
  end
  def notify_something
  end
end
class LogRunTime
  def call
    log "Job was running for X seconds"
  end
end

class LogRunTime
  def initialize(job, args = {})
    @job = job
  end
  def call
    log "Job was running for #{@job.run_time} seconds"
  end
end

job = Job.new
job.run(:running, :defragmentation)


def aasm_event_failed(event_name, old_state_name)
end

def set_process(name)
  logger.info "from #{aasm.from_state} to #{aasm.to_state}"
end






```

```
```

```
```
