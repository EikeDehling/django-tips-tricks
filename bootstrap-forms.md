# Bootstrap Forms

Bootstrap is a nice css toolkit for styling user interfaces on websites. There is options for integrating with Django, especially for outputting bootstrap styled forms.

## Including Bootstrap CSS

To include the bootstrap CSS, you need to add it to your static files (or use it from a CDN).

```
<link rel="stylesheet" type="text/css" href="{% static 'css/bootstrap.min.css' %}">
```


## Bootstrap forms

To easily output django forms with bootstrap styling, you can use a plugin:

```
{% load bootstrap3 %}

...

<form method="post" class="form-horizontal" enctype="multipart/form-data">
  {% csrf_token %}

  {% bootstrap_form form layout='horizontal' %}

  <div class="form-group">
    <div class="col-md-offset-3 col-md-9">
      <button class="btn btn-default" onclick="window.history.back()">Cancel</button>
      <button type="submit" class="btn btn-primary">Save</button>
    </div>
  </div>
</form>
```

This will output all your usual form elements, with bootstrap styling.


## Widgets

For example for date and time input, bootstrap plugins offer very nice UI/UX options.  You can add a dropdown to choose the date from a calendar for example.

Thing is, it would be nice to include that straight from the Django forms.

That is possible, with some tricks:


```
DatePickerInput = forms.DateInput(attrs={
    'autocomplete': 'off',
    'data-provide': 'datepicker',
    'data-date-format': 'yyyy-mm-dd',
    'data-date-autoclose': 'true'
})

TimePickerInput = forms.TimeInput(attrs={
    'autocomplete': 'off',
    'data-provide': 'timepicker',
    'data-show-meridian': 'false'
})


class JobForm(forms.ModelForm):
    date = forms.DateField(
        label='Job Date',
        widget=DatePickerInput
    )
```

This way, your django form easily renders the date form field, with the date picker plugin enabled!

