slackbot-api
====
![Travis CI](https://img.shields.io/travis/mdibaiee/slackbot-api.svg)
![Codecov](https://img.shields.io/codecov/c/github/mdibaiee/slackbot-api.svg)
![GitHub](https://img.shields.io/github/downloads/mdibaiee/slackbot-api/latest/total.svg)

Simple, understandable Slack Bot API.

#initialize

```javascript
import Bot from 'slackbot-api';
let bot = new Bot({
  token: process.env.SLACK_BOT_TOKEN // YOUR TOKEN HERE
});
```

#hear
Listen on all incoming messages matching a pattern.

```javascript
bot.hear(/hi (.*)/, message => {
  let name = message.match[1]; // message.match = message.text.exec(regex);

  message.reply('Hello!');
})
```

#listen
Listen on all incoming messages mentioning the bot (with or without @)

```javascript
bot.listen(/help/, message => {
  message.reply('You\'ve come to the right person!');
});
```

#sendMessage
```javascript
bot.sendMessage('general', 'Hello guys! wassup?');
bot.sendMessage('general', 'Hello', {
  unfurl_links: false,
  // extra parameters, see https://api.slack.com/methods/chat.postMessage
});
```

#deleteMessage
```javascript
let msg = await bot.sendMessage('general', 'Hello guys! wassup?');
bot.deleteMessage('general', msg.ts);
```

#updateMessage
```javascript
let msg = await bot.sendMessage('general', 'i can haz cakez');
bot.updateMessage('general', msg.ts, 'Yarrrrr!');
```

#react
Add reactions to messages.
```javascript
bot.listen(/rocket/, message => {
  message.react('rocket');
})

bot.react('general', msg.ts, 'rocket');
```

#icon
Set bot's profile icon.

```javascript
bot.icon('warning');
```

#random
Choose an argument randomly. Arguments may also be arrays.

```javascript
bot.listen(/hey/, message => {
  message.reply(bot.random('Hi', 'Hello', 'Wassup'));
})
```

#on
Listen on events.

```javascript
bot.on('channel_joined', event => {
  bot.sendMessage(event.channel.id, 'Hello guys! Thanks for inviting me.');
});
```

#find
Find a channel, user, IM, whatever by it's id or name.

```javascript
let user = bot.find('mdibaiee');
let channel = bot.find('general');
let group = bot.find('my-secret-group');
let byId = bot.find('U0123456');
```
