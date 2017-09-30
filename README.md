## Django and Django-Rest-Framework Antipatterns

_“Only a fool learns from his own mistakes. The wise man learns from the mistakes of others.” ― Otto von Bismarck_

I've been programming Django for about six years now, so I've learned a lot (mostly the hard way, many of my own fault). 

### What is an antipattern?
[Per sourcemaking.com](https://sourcemaking.com/antipatterns) "An antipattern is a literary form that describes a commonly occurring solution to a problem that generates decidedly negative consequences."

### How do they happen?
* No ramifications at the time of implementation, but long term increased complexity.
* Seems like a good idea at the time. Doesn't seem hacky.
* "Already happens this area of the code. Let me just use this somewhere else ..."
* "This one line solves all my problems! I don't have to refactor!"

### Why does it matter?
Django is a phenomenal framework that lets you build stable web end development quickly. However, an antipattern implemented with best intentions can become unwieldy. [What Technical Debt Feels Like](https://twitter.com/eylerwerve/status/907701103281807362)

#### Avoiding Antipatterns Helps With: 

* Corner case after corner case.
* Hotfixes for something that "[worked on my machine](https://i2.wp.com/www.developermemes.com/wp-content/uploads/2013/12/Worked-Fine-In-Dev-Ops-Problem-Now.jpg?fit=400%2C299)" 
* Implenting features that always requiring fixing other bugs completely unrelated 
* Poor testing practices.

# Antipatterns
## **Signals**

[Django Docs on Signals](https://docs.djangoproject.com/en/1.11/topics/signals/). Signals are sometimes useful, but I have been burned so many times from things magically getting called that they are rarely worth the additional implementation cost. [See : Lincoln Loop's post](https://lincolnloop.com/blog/django-anti-patterns-signals/)

## **Business Logic in models.py**

All models start off pretty simple. Example: Dealership Inventory Management Software

``` python
class Car(models.Model):
    name = CharField()
    year = CharField()
    created = DateTime(auto_now_add=True)
```
    
The problem that frequently results is business logic is slowly introduced bit by bit. Eventually the file becomes so tightly coupled refactoring becomes too intimidating. 

**Day One**

Product Manager : I want to know which cars are sold.

Engineer 1 : I'll add a time-sold, sold-at field and use that. I don't have to make a new model (CarsSoldRecord).

``` python
class Car(models.Model):
    name = CharField()
    year = CharField()
    created = DateTime(auto_now_add=True)
    time_sold = DateTime(null=True, blank=True)
    sold_at = DecimalField(null=True, blank=True)
```

**Day Two**

## Model Managers
## Dynamic Key Constants (Oxymoron)
## Passing Objects into Celery
## Differences in Staging, Production and Dev
## Indiscriminate Use of Pip Packages
## Indiscriminate Use of Middleware
## Not Squashing Migrations
## Using Email as an Error Log
## Not Adding Logging to All Components
## Tests Sharing Base Constants
## Overriding Django's Functions
## Taking Advice from HN as Gospel
## Pages Reliant on External APIs
## Nested Filters filter(cat__animal__zoo__state="New York)
## urls.py Nested Spaghetti
## Not Naming Automatic Migration Files
## Using settings_local and common mistakes
## settings.py Not Split Orthogonally 
## Custom Admin Inlines Spectrum
## Don't Use Middleware Components That Rely On Sync Requests

