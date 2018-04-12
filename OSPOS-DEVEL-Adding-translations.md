The translation process are made by two ways. In normal way translations are made in a web interface, an later this interface API integrates to github.

1. New strings must be added manually to each file in `language` directory and then the interface will sync those new strings.
2. Already untranslated string are not added manually to the files in language directory, must be made in the interface.

That interface its named [Weblate (http://weblate.jpeelaer.net)](http://weblate.jpeelaer.net) and sign up to help translating this fine application. After registering you can subscribe to different languages and you will be notified once a new translation is added.

[![Translation status](http://weblate.jpeelaer.net/widgets/ospos/-/svg-badge.svg)](http://weblate.jpeelaer.net/engage/ospos/?utm_source=widget)

## Translation status

[![Translation status](http://weblate.jpeelaer.net/widgets/ospos/-/multi-green.svg)](http://weblate.jpeelaer.net/engage/ospos/?utm_source=widget)

* [DOCS USERS Getting Started usage](DOCS-USERS-Getting-Started-usage)
* [OSPOS Complete feature list](OSPOS-complete-feature-datasheet)

# Translations Guideline

**WIP**

While not all guidelines will apply straight to all languages, we'd like to propose a few "Translation Guidelines" to be used and recommended for all translations:

- Titles follow capitalization rules for title format.  That is first Letter of each word capitalized except unimportant words and no punctuation is used (e.g., not "Change password." but instead "Change Password"). 
- Sentences follow sentence grammar rules for punctuation and capitalization specific to the language (e.g., not "one or more of the has processed sales or you are trying to delete your account" but instead "one or more of the has processed sales or you are trying to delete your account.").
- When sentences reference a field, it is referred to in the exact same format as the field (e.g., not "the title is a required field" but instead "Title is a required field").
- Use a consistent success/failure message format.  Currently, I see "The {field} was successfully updated" and in other places "{field} update successful", but I think we should stick to "{field} update successful" and {field} update failed" style messages.  There are three major reasons for this: Succinct translations, consistency and it allows us to remove dozens of translated lines because we only need one translated line for "update successful" and "update failed"  or "is a required field." and in the code we can call the field name and either update successful or failed.  Of course there will be exceptions where we want to add more information, and for those we can have a separate translation line.
- Gift Card(s) in the translation should be two words.  In the code it is one word, but English and most other languages it is two words.

# Translation in the "old way" (pre 3.0.0)

In order to add a translation below steps should be followed (German is an example in this case):

- Edit the CSV files in the `translations/` folder by adding a column for German at the end and a new translation on each row
- The language identifier must be one from `application/language/Language code definition` (be careful to do not simply select de because as far as we are aware, for instance, German from Germany is not fine with Germans from Switzerland and viceversa)
- Once you are done with all the files in /translations, run `php generate_languages.php` from the root of the project in a command line prompt which will create a de or de-xx dir in /application/language/
- Edit `application/views/configs/locale_config.php` and add German to `form_dropdown('language', something like 'de' => 'German', or 'de-DE' => 'German (Germany)'`
- Go to Store Config and Locale tab and select German
- Make a pull request based on the latest master. This pull request should contain the modified CSV files, the generated PHP language files and the updated locale_config.php.