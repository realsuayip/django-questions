# Django Questions


Here are some questions (of my taste) related to Django that I think are useful
to ponder upon. They are not interview questions per se, but I think it could be
a measure to reason your competence by checking yourself with each question.
Some of them constitute a bigger problem and therefore require a little thinking
where others could be answered immediately or dwell upon some implementation
details.

If you have any suggestions, feel free to add your question via a PR, however I
would only accept questions that follow the *theme* and are a bit *qualified*.


---


1. To improve update queries in the application, the project manager creates a
task which entails replacing model `save()` calls with
`save(update_fields=[...])`. After the task is completed, the client starts to
complain about outdated content (i.e., seeing the same content all the time) on
various endpoints. What could be the issue?

2. Two developers are working on the same model in separate branches. Developer
A finishes his work and his branch is merged to main. After some time, developer
B finishes his work, and to make sure there were no conflicts with B, he rebases
their branch from main; there appears to be no conflicts and branch of B is
merged. The main branch is then submitted to development server, where the auto
migrate commands fails due to conflicting migrations. What happened?

3. How would you add a unique field (say UUID) to a model, in a backwards
compatible manner?

4. In the following code, what might be the reason for the usage of
`transaction.atomic`?
   ```python
   @transaction.atomic
   def commit(instance, data):
       for attr, value in data.items():
           setattr(instance, attr, value)
       instance.save(update_fields=data.keys())
    ```

5. A developer uses a many-to-many field with `"self"` to hold "following users"
of a user. After using `add` method on the field, they realize that the target
user's following list is also populated. What might have caused this?

6. Could you describe a scenario in which a recursion error is propagated
through signals? Assume that a signal does not directly invoke itself.

7. What is the difference between psycopg2 and psycopg2-binary? Which one should
be used in which case?

8. Which library do you need to install to use `models.ImageField`?

9. What is 'gunicorn'?

10. The code below produces incorrect counts for specified fields. What could be
the reason?
    ```python
    User.objects.annotate(Count("following"), Count("followers"))
    ```

11. Explain the distinction between `FieldFile` and `FileField`.

12. Why do some developers advocate the use of `default=timezone.now` over
`auto_now_add=True`?

13. How does `manage.py` determine the settings module of your application?

14. What is the difference between Django-provided `TestCase` and
`TransactionTestCase`?

15. How would you handle a multi-language Django project? Which Django tools and
3rd party libraries would you use?

16. Could you tell of some built-in security measures taken by Django? Do you
know of a common security consideration, in the context of the web, that Django
does not provide?

17. Why adding `null=True` to a `CharField` is a bad idea?

18. You are asked to build a "soft-deletion" implementation that would encompass
multiple models across multiple apps. In general terms, how would you do it?

19. Say you have a field which has a `RegexValidator`. How would you impose this 
validation at the database level as well, without using raw SQL?

20. Say you are coding in a context where it is not possible import
the desired model class due to circular imports. How would you acquire this
model class?

21. Other than omitting `prefetch_related` and `select_related`, what are some
common mistakes developers make that slow down Django applications?

22. You are assigned to monitor a Django application in production; your aim is
to find possible bottlenecks and optimize overall performance of the
application. What tools are you going to use? By giving example cases, what type
of solutions could you implement?

23. What is 'middleware'? Can you name some middleware classes that are provided
by Django, with their purpose? Could you tell of an example where you needed to
use a middleware?

24. Clients complain about the slowness of the Django admin site. What could be
the reasons behind this issue, and how would you improve it?

25. Can you differentiate model methods and model manager methods? In what cases
using one suits better than the other?

26. One could hook up the `post_save` signal to do processing after the model
instance is saved, it is also possible to override `save()` model method to do
the same work. Which method would you use in which case?

27. If you omit `related_name` on a `ForeignKey` field, what does Django set as
default?

28. A developer converts `ForeignKey` with `unique=True` to `OneToOneField`,
knowing these two correspond to the same structure in the database. Would this
conversion break anything in the domain of Django? If so, how?

29. In QuerySets, what is the difference between using one filter with many
arguments versus chaining multiple filters?

30. What does the phrase “QuerySets are lazy” mean? Give some instances where a
QuerySet would get evaluated.

31. How would you ensure an email is sent only after an object is created in
the database, and how would you test this functionality?

32. Do you know how Django development team manages its releases? Which version
of Django would you use at any given time, and why?

33. What do you think about generic relations? Can you tell few pros and/or
cons?

34. Django is often considered to have a monolithic architecture, what does this
mean?

35. Give an instance from Django APIs where operator overriding is used.

36. What does `F` object do in Django? Give a couple of distinct cases where the
usage of `F` object would be appropriate. 

37. Explain Cross-site request forgery (CSRF) vulnerability and Django's
secure implementation against it.

38. Explain BREACH attack. Does Django have any mitigation against it? How
would such mitigation work?

39. Assume that you are adding a new setting, which should hold some sort of
secret such as an API key. Security-wise, in what manner would you add that key
so that it would be more secure i.e., not easily exposed to outside?

40. You are doing a security audit for a Django website, and by checking
"Not found" page, you have realized that the website has not disabled the
`DEBUG` mode. To make your point, you want to trigger a 500 error so that all 
the environment variables would be exposed; in which case you would send the
exposed variables to the customer in joy. How would you trigger a 500 error
easily, in this case?

41. What are some things that make apparent that a website uses Django as backend?

42. In the context of database backup, why is the usage of  Django management
commands`loaddata` and `dumpdata` are not desirable? What would a proper database
backup setup entail?

43. In summary, how does Django migrations work? Why do we need migrations? Do
you know what happens in the background? What does Django migrations entail in
the actual database?

44. How do you scale a Django application?

45. What is WSGI; how about ASGI?

46. Using Django, how would you transfer some data via untrusted environments
(e.g., email), making sure of the authenticity and integrity of the data while
receiving it?
