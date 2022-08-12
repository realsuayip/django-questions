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
