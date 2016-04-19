# Writing issues

When filing issues, keep the title short and the body descriptive.

<br>

* **Keep the title short.**<br>
  Put any details in the body, not in the title. This makes it easier to digest a long list of issues.

  > `When I try to change passwords, an error is raised.` ✗ *...can be shorter*<br>
  > `[User] can't change passwords` ✗ *...put that in the description*<br>
  > `Can't change passwords` :+1:
  
* **Write a short description.**<br>
  Add a one-sentence (or one-paragraph) in the body of the issue.

  > 
  > Title: `Can't change passwords`<br>
  > Description:
  > `When I'm logged into as a User, the "change email" form returns an error.`

<br>

## Details

* **Be visual.**<br>
  Include screenshots when possible!

* **Be detailed.**<br>
  For bug reports, ensure that the following details are available or are obvious:

  * URL *(if applicable)*
  * Environment *(OS, browser, website environment)*
  * Steps to reproduce
  * Expected result
  * Actual result
  
* **But not too detailed.**<br>
  You don't need to actually list *all* of them (especially for simple issues), just make sure that anyone can figure those details out.

* **Don't be too general.**<br>
  Try to be more specific when possible.

  > `Products error`  ✗ *...too broad*<br>
  > `Can't buy products` ✗ *...still too broad*<br>
  > `Product page error` ✗ *...still too broad*<br>
  > `Product page: the buy button isn't clickable` :+1:

<br>

## Short example
No need to include steps/expected/actual when it's obvious.

> **Avatars are not shown**<br>
> The user directory is missing avatars. (OS X, Firefox, Production)<br>
> http://ticketadvisor.com/users
>
> `[screenshot goes here]`

## Full example

> **Can't send email**<br>
> The "send email" button isn't clickable.<br>
> Environment: OS X, Firefox, Production.<br>
> http://ticketadvisor.com/user/23/edit

> `[screenshot goes here]`
  
> Steps:<br>
  1. Log in as a user<br>
  2. Go to the Inbox page<br>
  3. Click "write new email"<br>
  4. Click "send"<br>
  
> Expected: The email will be sent.<br>
> Actual: A JavaScript error appears when "send" is clicked.
