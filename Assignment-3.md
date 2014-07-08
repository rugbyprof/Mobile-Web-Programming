### Assignment 3 - First Simple Web Page.
#### Due: July 11th by 1300 hours.

-----

#### Dynamic Contact Card

In your `index.php` file, add the code snippet:

```php
<?php
  if(!isset($_POST['submit'])){
?>
      <form name="input" action="index.php" method="post">
      Username: <input type="text" name="user">
      <input type="submit" name="submit" value="Create">
      </form>
<?php
  exit;
  }
?>
```
