# How to add translations

In order to add a translation below steps should be followed (German is an example in this case):

- edit the files contained in /translations adding a column for German and of course translation for each line
- the language identifier must be one from /application/language/Language code definition (be careful to do not simply select de because as far as we are aware, for instance, German from Germany is not fine with Germans from Switzerland and viceversa)
- once you have done with all the files in /translations, run /generate_languages.php which will create a de or de-xx dir in /application/language/
- edit application/views/configs/locale_config.php and add German to form_dropdown('language', something like 'de' => 'German', or 'de-DE' => 'German (Germany)'
- to state the obvious here, go to Store Config and Locale tab and select German
- make a pull request containing the changes in the csv files, the generated language files and the updated locale_config.php.