THIS_GIT_REPO_NAME

REQUIREMENTS
--------
* heroku [account](https://www.heroku.com/) and [toolbelt](https://toolbelt.heroku.com/)
* python
   * [pip](https://pypi.python.org/pypi/pip)
   * cherrypy (```pip install cherrypy```)
   * Twython (```pip install Twython```)

INSTRUCTIONS
--------
0. Fork and pull this repo.

1. In local repo, create a new heroku app.
    * ```heroku create --stack cedar```
    * ```heroku apps:rename YOUR_APP_NAME```

2. Create a [new twitter account](https://twitter.com/).
    * Instead of creating a new email account, add [a tag](http://en.wikipedia.org/wiki/Email_address#Address_tags) to an existing email account
       - Ex: _email@gmail.com_ => _email+twitterbot@gmail.com_
    * Confirm the email address associated with your new twitter account.

4. Create a [new twitter app](https://dev.twitter.com/apps).
    * Under _Settings_ / _Application Type_:
        - Enable _"Read and Write"_
        - Check _"Allow this application to be used to Sign in with Twitter"_

5. Create environment variables.
    * in local repo: update ```.env``` with your twitter app keys
        - ```TWITTER_CONSUMER_KEY=replace_this```
        - ```TWITTER_CONSUMER_SECRET=replace_this```
        - ```TWITTER_OAUTH_TOKEN=replace_this```
        - ```TWITTER_OAUTH_TOKEN_SECRET=replace_this```
    * on [heroku](https://devcenter.heroku.com/articles/config-vars): use ```heroku-config``` to copy contents of ```.env```
        - ```heroku plugins:install git://github.com/ddollar/heroku-config.git```
        - ```heroku config:push```
        - NOTE: to update heroku environment variables later, run ```heroku config:push --overwrite```
        - OR: add heroku environment variables manually using ```heroku config:set YOUR_ENV_VAR=replace_this```

6. Update the function ```get_message()``` in ```model.py``` to create your bot's tweets.
    * ```foreman start``` tests your heroku app locally.
    * Opening the url ```0.0.0.0:5000``` should now make your bot tweet.

7. Push local changes to heroku and github.
    * ```git push heroku master``` pushes all commits to heroku.
    * Opening the url ```YOUR_APP_NAME.herokuapp.com``` should now make your bot tweet.

8. Automate your bot.
   * Set up a cron job using [easycron](http://www.easycron.com/user) that calls ```YOUR_APP_NAME.herokuapp.com``` as often as you'd like your bot to tweet.
    * NOTE: You will have to renew your account once a month to keep it free.