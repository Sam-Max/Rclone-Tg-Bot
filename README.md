# Heroku Deploy

**Important Notes**
1. Add the private files (config.env, rclone.conf) in heroku branch not in master.
2. Don't add variables in heroku Environment, you can only add `CONFIG_FILE_URL`.
3. Don't deploy using hmanager or github integration.
5. If you want to edit anything in code, so u should edit [h-code branch](https://github.com/Sam-Max/Rclone-Tg-Bot/tree/h-code). After that u should add fill `UPSTREAM_REPO` of your fork and leave `UPSTREAM_BRANCH` empty since it's by default `h-code`.

------

## Deploy With CLI

- Clone this repo:
```
git clone https://github.com/Sam-Max/Rclone-Tg-Bot rctgbot/ && cd rctgbot
```
- Switch to heroku branch
  - **NOTE**: Don't commit changes in master branch. If you have committed your changes in master branch and after that you switched to heroku branch, the new added files(private files) will `NOT` appear in heroku branch.
```
git checkout heroku
```
- After adding your private files
```
git add . -f
```
- Commit your changes
```
git commit -m token
```
- Login to heroku
```
heroku login
```
- Create heroku app
```
heroku create --region us YOURAPPNAME
```
- Add remote
```
heroku git:remote -a YOURAPPNAME
```
- Create container
```
heroku stack:set container
```
- Push to heroku
```
git push heroku heroku:master -f
```

------

### Extras
```
- To delete the app
```
heroku apps:destroy YOURAPPNAME
```
- To restart dyno
```
heroku restart
```
- To turn off dyno
```
heroku ps:scale web=0
```
- To turn on dyno
```
heroku ps:scale web=1
```
- To set heroku variable
```
heroku config:set VARNAME=VARTEXT
```
- To get live logs
```
heroku logs -t
```

------

## Deploy With Github Workflow

1. Go to Repository Settings -> Secrets

2. Add the below Required Variables one by one by clicking New Repository Secret every time.

   - HEROKU_EMAIL: Heroku Account Email Id in which the above app will be deployed
   - HEROKU_API_KEY: Your Heroku API key, get it from https://dashboard.heroku.com/account
   - HEROKU_APP_NAME: Your Heroku app name, Name Must be unique
   - CONFIG_FILE_URL: Copy [This](https://raw.githubusercontent.com/anasty17/mirror-leech-telegram-bot/master/config_sample.env) in any text editor.Remove the _____REMOVE_THIS_LINE_____=True line and fill the variables. For details about config you can see Here. Go to https://gist.github.com and paste your config data. Rename the file to config.env then create secret gist. Click on Raw, copy the link. This will be your CONFIG_FILE_URL. Refer to below images for clarity.

3. Remove commit id from raw link to be able to change variables without updating the CONFIG_FILE_URL in secrets. Should be in this form: https://gist.githubusercontent.com/username/gist-id/raw/config.env
   - Before: https://gist.githubusercontent.com/anasty17/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/19ba5ab5eb43016422193319f28bc3c7dfb60f25/config.env
   - After: https://gist.githubusercontent.com/anasty17/8cce4a4b4e7f4ea47e948b2d058e52ac/raw/config.env

4. Add all your private files in this branch or use variables links in `config.env`.

5. After adding all the above Required Variables go to Github Actions tab in your repository.
   - Select Manually Deploy to Heroku workflow.

6. Choose `heroku` branch and click on Run workflow.
