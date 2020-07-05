The password app lists official clients, third party apps and programming libraries in the included "Apps & Extensions" section.
Apps are also listed in the readme, libraries are also listed in the developer handbook.
If you have developed an app or library and want it to be listed there, this page lists what you need to do.

## Requirements
Your app should meet these requirements.

#### Open Source
The source code of your app must be public.
Since security and trust are very important to our users, they must be able to check the source code of the applications they use.

**Note:** This does not mean that your app must be free or that others must be allowed to use your source code.

#### No Ads
Any app must not contain any ads.
Any tracking must be optional and _opt-in_ and compliant with the EU GDPR.

#### Optional third party services
If your app contacts any server other than the Nextcloud instance of the user, this action should be optional.
The user must also be aware if data is sent to another service.

#### No legacy api
We do not accept any app that uses the legacy api.


## How to list your app
If you want to have your app listed, please [create a ticket in our issue tracker](https://github.com/marius-wieschollek/passwords/issues/new?labels=feature&template=Feature_request.md).

The ticket must contain the following:
* Name of your app
* Short description of your app (optional in multiple languages)
* Logo of your app (SVG, PNG or JPG, ca 400x400px) (only apps, not libraries)
* Link to the website/store where users can get your app
* Link to the sources
* Supported Systems/Browsers etc.
* Information how we can test your app