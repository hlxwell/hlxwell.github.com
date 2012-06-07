---
layout: post
title: "use ActiveSupport::Configurable to store config options"
category: 
tags: []
---
{% include JB/setup %}

{{ highlight ruby }}
class Employee
  include ActiveSupport::Configurable
  config_accessor :research_lab_entry, :paid_leave
  
  # The config options are now also available as: 
  # employee.research_lab_entry
  # employee.paid_leave
end
{{ end highlight }}


{{ highlight ruby }}
# Set the config option at the class level
Employee.config.paid_leave = 5

# Create a new object and check the value
employee = Employee.new
employee.config.paid_leave # => 5

# Set a new value at the object-level
employee.config.paid_leave = 3

# Now check the value at the class level
Employee.config.paid_leave # => 3
{{ end highlight }}