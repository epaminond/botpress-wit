# botpress-wit

The easiest way to create a Wit.ai bot with Botpress

## Getting started

```
botpress install wit
```

The Wit.ai module should now be available in your bot UI

## Features

This module has two modes: **Understanding** (message API) and **Stories** (converse API).

### Understanding

This mode will inject understanding metadata inside incoming messages through the Wit.ai middleware.

Events will have a `wit` property populated with the extracted `entities` and the `context`.

**Tip:** Use this mode if you want to handle the conversation flow yourself and only want to extract entities from incoming text. This is great for programmers.

```js
bp.hear({'wit.entities.intent[0].value': 'weather'}, (event, next) => {
  console.log('>> Weather')
  bp.messenger.sendText(event.user.id, 'Weather intent')
})
```

### Stories

This mode will run your Wit.ai stories automatically given that you defined the **Actions** in botpress.

For more information about Actions and how they are run, make sure to read [node-wit](https://github.com/wit-ai/node-wit)'s documentation.

**Tip:** Use this mode if you created a conversation flow on Wit.ai's User Interface and want it to run automatically in your bot. This is great for non-programmers.

#### Example

```js
// Implement your Actions like this
bp.wit.actions['getWeather'] = request => {
  return new Promise((resolve, reject) => {
    bp.logger.info('Get Weather called', request)
    // Do something here
    resolve(request.context)
  })
}

// You need to call this method once you are done implementing the Actions
bp.wit.reinitializeClient()
```


## Community

Pull requests are welcomed! We believe that it takes all of us to create something big and impactful.

There's a [Slack community](https://slack.botpress.io) where you are welcome to join us, ask any question and even help others.

Get an invite and join us now! 👉[https://slack.botpress.io](https://slack.botpress.io)

## License

botpress-wit is licensed under [AGPL-3.0](/LICENSE)
