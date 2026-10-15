# Part 2: use Acceptance Tests to get new scenarios passing

---------- 
We've provided three Cucumber scenarios in the file `features/movies_by_director.feature` to drive the creation of 2 happy paths and 1 sad path of Search for Movies by Director.

**The first lets you add director info to an existing movie**

This part doesn't require creating any new views or controller actions, but does require
modifying existing views, and will require creating a new step definition and possibly adding a line or two to `features/support/paths.rb`.

To get the scenario to pass, focus on **one line (step) at a time, in order**, and write just the code to make that step pass.

Tip: if you want to focus on running only a single scenario at a time, you can say `cucumber features/movies_by_director.feature:NNN` where NNN is the starting line number (containing the `Scenario:` keyword) of the specific scenario you want to run, or `cucumber features/movies_by_director.feature -n "STRING"` where `STRING` is a substring of the name(s) of the scenario(s) you want to run (again as specified by the `Scenario:` line of each one).

**The second scenario tests what happens when you click "Find Movies With Same Director" on a movie's detail page.**

The link should result in landing on a new page, "the Similar Movies page", listing all movies that share the same director as the previously displayed movie.  

* For the first line in that scenario, you'll have to modify the existing Show Movie (details) view to add the link.  Note that you can get this step to pass as long as the link's destination is a valid URL---you _don't_ have to setup the real target page for it yet. This is part of the BDD process, allowing you to do one step at a time: you can just focus on making sure the link appears and is clickable by using any valid URL, _then_ go on to creating the correct page for it to land on (as required for the _next_ scenario step to pass).

* You'll need to choose a RESTful route name for this new action ("show movies with similar director") and you'll have to add a route, view and controller method for it.  One suggested route might be `GET /movies/:id/similar` where `:id` is a route param that will match the ID of the movie whose director you want to match.  (Hint: since this route isn't created as one of the default routes by `resources :movies`, check the syntax for "Non-Resource-Based Routes" in the [Rails Routing documentation](http://guides.rubyonrails.org/routing.html).)

* You will need to a method in the `Movie` model to find movies whose director matches that of the current movie. The controller action that handles the new route will call that model method.

<details>
  <summary> Would this model method be a class method or instance
  method?  </summary> 
  <p><blockquote> Technically it could be either.
  You could call it on a movie, the idea being that it returns other
  movies with the same director as its receiver,
  e.g. <code>movie.others_by_same_director()</code>.  Or you could
  define it as a class method,
  e.g. <code>Movie.with_director(director)</code>. In fact, it's great
  practice to write it both ways.  But either is fine in this
  assignment.
  </blockquote></p>
</details>

* For the Cucumber scenario to find the new page, you will likely also need to modify `features/support/paths.rb` to recognize the Cucumber "plain language" name of this new route, as referenced by the scenario step "I should be on the Similar Movies page for....".

**The third scenario handles the sad path.**

When the current movie has no director info but we try to do "Find with same director" anyway, then we should redirect to the list of all movies page and display a helpful message.

**HINT:** Use the `flash[]` to store a message, and in the list of all movies, conditionally display the value of the appropriate `flash[]` key if it's non-empty.  Using the Bootstrap CSS classes `alert alert-info` or `alert alert-warning` on the message-display element will display it in a color-highlighted box.

Success for this part is getting all scenarios to pass.

---

[← Part 1: add a Director field to Movies](02-Part-1--add-a-Director-field-to-Movies.md) | [Contents](README.md) | [Part 3: Code Coverage →](04-Part-3--Code-Coverage.md)
