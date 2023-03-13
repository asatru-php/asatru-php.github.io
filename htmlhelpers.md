# HTML helpers

The Html helper class <i>Html</i> can be used to programmatically render HTML elements into the 
document. It provides the following methods:
```php
//Specify the HTML tag name and an array of key-value paired attributes. Returns a string containing the HTML element.
renderTag(name, attr)

//Closes a previously began HTML tag. Returns the closed HTML tag string
renderCloseTag($name)
```

This is how you could use it in your view:
```php
{!! Html::renderTag('div', ['class' => 'my-class', 'onclick' => 'window.alert("Hello World!");']) !!}
{!! Html::renderCloseTag('div') !!}
```

You can also just use renderTag() for single HTML tag elements:
```php
{!! Html::renderTag('img', ['class' => 'my-image-class', 'src' => asset('img/my-image.png'), 'alt' => 'Alt text']) !!}
```

You can create own Html helper classes based on the Html class.

One of the derived helper classes is the Form class. It assists you in rendering forms. It provides the following methods:
```php
//Begins a new form. You can additionally specify attributes. Returns the opened form element string
begin(attr)

//Puts a form element into the form, such as input, textarea, etc. Specify attributes with the attr param
putElement(name, attr)

//Closes an open element previously added with putElement(). Not needed for single elements
closeElement(name)

//Closes the form
end()
```

A usage example could be:
```php
{!! Form::begin(['method' => 'POST', 'action' => url('/my/endpoint'), 'enctype' => 'multipart/form-data']) !!}
@csrf
{!! Form::putElement('input', ['type' => 'text', 'name' => 'name', 'placeholder' => 'My placeholder', 'required' => null]) !!}
{!! Form::putElement('textarea', ['name' => 'description', 'placeholder' => 'My placeholder']) !!}
{{ 'My textarea content' }}
{!! Form::closeElement('textarea') !!}
{!! Form::putElement('input', ['name' => 'file', 'type' => 'file']) !!}
{!! Form::putElement('input', ['type' => 'submit', value => 'Submit form']) !!}
{!! Form::end() !!}
```

Note the required param which is set to null. This will create a required attribute without a value.