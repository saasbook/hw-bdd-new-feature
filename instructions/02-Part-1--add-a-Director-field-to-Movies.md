# Part 1: add a Director field to Movies

---------


Create and apply a migration that adds the `director` field to the movies table. The `director` field should be a string containing the name of the movie’s director.

**Hint:** you may find useful the [`add_column` method of `ActiveRecord::Migration`](http://apidock.com/rails/ActiveRecord/ConnectionAdapters/SchemaStatements/add_column).

Remember that once the migration is applied, you also have to do `bundle exec rails db:test:prepare` to load the new post-migration schema into the test database.


<details><summary>
  Clearly, now that a new field has been added, we will have to modify the Views so that the user can see and enter values for that field. Do we also have to modify the model file in order for the new field to be "noticed"?
  </summary><p><blockquote>
  Nope. ActiveRecord infers the columns and their data types by inspecting the database. However, if we wanted to have a validation on that column, we'd have to specifically mention it in a <code>validates</code> call.
  </blockquote></p>
</details>


<details>
  <summary>
  Look at the step definitions for the failing steps of the Cucumber scenarios. (Where would you find those definitions?) Based on the step definitions, which step(s) of the scenario file would you now expect to <b>pass</b> if you re-run Cucumber, and why?
  </summary>
  <p><blockquote>
  Once this field is added, running <code>bundle exec cucumber</code> should allow the <code>Background:</code> steps to pass, since they just use ActiveRecord directly to create movies with a director field.  But the other scenarios all manipulate the user interface (the views), which you have not yet modified, so they will still fail.
  </blockquote></p>
</details>


Verify that the Cucumber steps you expect to pass actually do pass.

<details>
  <summary>
  If you're still with us, the background steps now pass, but the very
  first step of each scenario fails, because you're asking Cucumber to
  "visit a page" but you haven't provided a mapping between the
  human-readable name of the page (e.g. <code>the edit page for "Alien"</code>)
  and the actual path (URL) that would go to that page in
  RottenPotatoes.  Where will you need to add this mapping (in what
  file and what method in that file)? (Hint:
  read the error message carefully, and look for the implementation of the
  <code>When I visit...</code> step def.)
  </summary>
  <p><blockquote>
  The step def  just calls the underlying Capybara
  method <code>visit</code>, but relies on a method called <code>path_to(...)</code> that is
  supposed to translate a plain-language phrase such as 'the edit page
  for "Alien"' into a URL.  In some cases, an argument in the
  plain-language phrase is captured and substituted into the URL.
  This is the method where you must add a clause to handle the new feature.
  </blockquote></p>
</details>


<details><summary>
  Besides modifying the Views, will we have to modify anything in the controller?  If so, what?
  </summary>
  <p><blockquote>
  Yes: we have to add <code>:director</code> to the list of movie attributes in the <code>def movie_params</code> method in <code>movies_controller.rb</code>.  Otherwise, even if that value is available as <code>params["movie"]["director"]</code>, it will be "scrubbed" by the <code>require</code> and <code>permit</code> calls on <code>params</code> before the controller actions are able to see it.
  </blockquote></p>
</details>


<details><summary>
  Which controller actions, specifically, would fail to work if we didn't make the above change?
  </summary>
  <p><blockquote>
  <code>create</code> and <code>update</code> would fail, since they are the ones that expect a form submission in <code>params</code> in which <code>params["movies"]</code> should appear.  The other actions do not expect or manipulate this form (and do not call the helper function <code>movie_params</code>) so they would not be affected.
  </blockquote></p>
</details>

Based on the above self-checks, you should be able to modify the controller and views as needed to be "aware" of the new `director` field.

---

[← Using BDD to Drive a New Feature](01-Using-BDD-to-Drive-a-New-Feature.md) | [Contents](README.md) | [Part 2: use Acceptance Tests to get new scenarios passing →](03-Part-2--use-Acceptance-Tests-to-get-new-scenarios-passing.md)
