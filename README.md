# Strict python

Strict python - adds checkers on input and output for python programs.

How do we do this? Idea is easy - when you write a docstring for a python function - you need to describe all incoming arguments, and if needed - describe a structure for each argument.

It's can be useful for **web development**. When we have incoming request - we need to make basic data validation on incoming data from user. If data doesn't much the described structure - we need to refuse access to this page and show error. 

Small example:
```python
# Assume it's Django function in views.py that handles
# user request and returns response.

@strict
def show_user(request):
  """Shows information about the given user.

  Args:
    request:
      POST:
        {
          user_id: int. User id.
          options: optional dict. Additional options.
            {
              additional_fields: optional list of integers.
              response_format: str choice from ["JSON", "HTML", "XML"]. In which format
                we need to return data.
            }
          welcome_phrase: optionsl str. Any string that will be printed before user name.
        }

  Returns:
    HttpResponse. It can be JSON/HTML/XML document inside the object.
  """
  user = get_user_by_id(request.POST['user_id'],
                        additional_fields=request.POST.get('additional_fields'))
  welcome_phrase = request.POST.get('welcome_phrase')
  if not welcome_phrase:
    welcome_phrase = "Hello"
  return HttpResponse('{} {}!'.format(welcome_phrase, user.username))
```
