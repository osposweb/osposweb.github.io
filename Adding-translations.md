# How to add translations for a new language

* you need to edit the files contained in /translations adding a column for German and of course translation for each line
* the language identifier must be one from /application/language/Language code definition (be careful to do not simply select de because as far as I am aware, for instance, German from Germany is not fine with Germans from Switzerland and viceversa - I dealt once in my life with German translations and people are not happy to read "the wrong version" - )
* once you have done with all the files in /translations you need to run /generate_languages.php which will create a de or de-xx dir in /application/language/
* you need to edit application/views/configs/locale_config.php and add German to form_dropdown('language', something like 'de' => 'German', or 'de-DE' => 'German (Germany)', and to state the obvious here, you need to go to Store Config and Locale tab and select German
* finally make a pull request containing the changes in the csv files, the generated language files and the updated locale_config.php.