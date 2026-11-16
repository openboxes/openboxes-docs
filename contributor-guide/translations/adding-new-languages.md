# Adding new languages

If the language you're trying to translate is not yet in OpenBoxes or Crowdin, the following instructions outline how to get the language added.

## Requesting a new language

If you're not a project administrator, get in contact with us by posting to the [OpenBoxes Slack](http://slack-signup.openboxes.com/), [adding a post to our community forums](https://community.openboxes.com/), or by [creating a new GitHub Issue](https://github.com/openboxes/openboxes/issues). Let us know the language that you'd like to translate and we'll get you set up as quickly as possible.

## Adding a new language

If you're a project administrator, the following are instructions on how to add a new langugage into OpenBoxes and make it translatable in Crowdin.

### Adding a language to Crowdin

Translated languages in Crowdin are known as "target languages". To add a new target language, navigate to the project settings > Languages, then simply select any new langugages that we want to support.

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

This should cause Crowdin to automatically create a pull request into the openboxes repository containing a new `messages.properties` file for the language.

See [Crowdin's documentation](https://support.crowdin.com/project-settings/languages/#target-languages) for additional information.

The following video covers everything required to configure Crowdin (plus also explains how the In-Context feature works):

{% embed url="https://www.youtube.com/watch?v=ktfw7UsW3qw" %}

### Adding a language to OpenBoxes

Edit the `application.yml` file and add the [two letter locale code](https://simplelocalize.io/data/locales/) of the new language to the `supportedLocales` property:

```
openboxes:
    locale:
        supportedLocales: [...]
```

After redeploying the application, the new language should be selectable in the list of locales in the website footer.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### Adding date translations to the frontend

The React frontend formats dates (month and day names, the date picker calendar) with [date-fns](https://date-fns.org/). To keep the bundle small, only the locales listed in `src/js/consts/dateFnsLocales.js` are included, so a new language also has to be added there. Otherwise dates on React pages will be displayed in English.

Check that [date-fns supports the language](https://github.com/date-fns/date-fns/tree/main/src/locale), then import its locale and add it to the exported object under the same code that you added to `supportedLocales`:

```js
import {
  ar, de, enUS, es, fi, fr, ht, it, nl, pt,
} from 'date-fns/locale';

const dateFnsLocales = {
  ar, de, enUS, es, fi, fr, ht, it, nl, pt,
};
```

If the date-fns locale has a different name than the OpenBoxes locale code (for example `zhCN` for `zh`), map it explicitly:

```js
const dateFnsLocales = {
  // ...
  zh: zhCN,
};
```

If date-fns doesn't support the language, skip this step. Dates for that language will fall back to English.
