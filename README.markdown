admin popups
====================
> if using grappeli, copy RelatedObjectLookups.js to your admin_media folder from django's admin media 

settings.py
--------------------
    TEMPLATE_CONTEXT_PROCESSORS = (
        'tekextensions.context_processors.admin_media_prefix',
    )
    INSTALLED_APPS = (
        'tekextensions',
    )


urls.py
--------------------
    url(r'^add/(?P<model_name>\w+)/?$', 'tekextensions.views.add_new_model'),

    or adding some custom form (the class, not string name)

    from path.to.custom.forms import CustomForm
    ...
    url(r'^add/(?P<model_name>\w+)/?$', 'tekextensions.views.add_new_model',
        {'form': CustomForm}),


forms.py
--------------------
>override any ModelChoiceField widget with SelectWithPopUp

    from tekextensions.widgets import SelectWithPopUp
    from django import forms
    
    class CustomForm(forms.Form):
        company = forms.ModelChoiceField(CustomModel.objects, widget=SelectWithPopUp)
        # or
        company = forms.ModelChoiceField(CustomModel.objects, widget=SelectWithPopUp(model=CustomModel))
