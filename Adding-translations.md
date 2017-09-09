# How to add translations

# Using Weblate (post 3.0.0)

Find our [weblate instance](http://weblate.jpeelaer.net) here and sign up to help translating this fine application. After registering you can subscribe to different languages and you will be notified once a new translation is added.

[![Translation status](http://weblate.jpeelaer.net/widgets/ospos/-/287x66-grey.png)](http://weblate.jpeelaer.net/engage/ospos/?utm_source=widget)

# Old way (pre 3.0.0) - deprecated

In order to add a translation below steps should be followed (German is an example in this case):

- Edit the CSV files in the `translations/` folder by adding a column for German at the end and a new translation on each row
- The language identifier must be one from `application/language/Language code definition` (be careful to do not simply select de because as far as we are aware, for instance, German from Germany is not fine with Germans from Switzerland and viceversa)
- Once you are done with all the files in /translations, run `php generate_languages.php` from the root of the project in a command line prompt which will create a de or de-xx dir in /application/language/
- Edit `application/views/configs/locale_config.php` and add German to `form_dropdown('language', something like 'de' => 'German', or 'de-DE' => 'German (Germany)'`
- Go to Store Config and Locale tab and select German
- Make a pull request based on the latest master. This pull request should contain the modified CSV files, the generated PHP language files and the updated locale_config.php.