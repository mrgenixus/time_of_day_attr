# time_of_day_attr

Convert time of day to seconds since midnight and back.

# Installation

```console
gem install time_of_day_attr
```

# Usage

```ruby
class BusinessHour < ActiveRecord::Base
  time_of_day_attr :opening, :closing
end

business_hour = BusinessHour.new(opening: '9:00', closing: '17:00')

business_hour.opening
 => 32400
business_hour.closing
 => 61200

TimeOfDayAttr.l(business_hour.opening)
 => '9:00'
TimeOfDayAttr.l(business_hour.closing)
 => '17:00'
```

You could also omit minutes at full hour:
```ruby
TimeOfDayAttr.l(business_hour.opening, omit_minutes_at_full_hour: true)
 => '9'
```

## Formats

The standard formats for conversation are:

```yml
en:
  time_of_day:
    formats:
      default: '%k:%M'
      hour: '%k'
```

You can overwrite them or use custom formats:
```yml
en:
  time_of_day:
    formats:
      zero_padded: '%H:%M'
```

```ruby
class BusinessHour < ActiveRecord::Base
  time_of_day_attr :opening, formats: [:zero_padded]
end

business_hour = BusinessHour.new(opening: '09:00')

business_hour.opening
 => 32400

TimeOfDayAttr.l(business_hour.opening, format: :zero_padded)
 => '09:00'
```

## time of day field

To get a text field with the converted value:
```erb
<%= form_for(business_hour) do |f| %>
  <%= f.time_of_day_field(:opening) %>
<% end %>
```

# License

This project uses MIT-LICENSE