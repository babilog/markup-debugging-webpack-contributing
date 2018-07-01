# Debugging Webpack for Beginner Contributors

I recently started to think about how I could contribute more to open source. I think that is a thought that we all as developers have come across once or twice in our careers. I mean, we use so much open source code, the idea of contributing back to the community seems like an easy task in itself right?

I took a look around to see what type of projects I would like to contribute to, and I decided to look first at the projects that I used the most in my day to day work or as part of my side projects.

Webpack seems to that project for me :)

## Intimidating Codebase

Thinking of Webpack as my first open source project to contribute towards felt extremely intimidating. Webpack in itself is massive, and has a rather healthy and strongly opinionated community around it (Nothing wrong with that of course). However, as an aspiring open source contributor, it certainly looked to me as a massive challenge to just understand how it worked under the hood so to speak.

## Debugging

This takes me to my first challenge, how the heck do I debug this massive codebase? After all, most of us consider debugging a codebase as the first step towards understanding the control flow and logic.

### Assumptions

I'm assuming that you already have a version of Webpack forked and cloned to your local machine. In my case, I forked the latest Webpack 3 branch.

`git checkout remotes/origin/webpack-3`

Then, you'll more than likely want to run either `npm i` or `yarn` to pull all the `node_modules` goodies.

### VSCode Setup

I'm assuming that you also are working in VSCode, so we'll want to setup our debug configuration.

Here's the minimum config you'll need to get started:

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attack-Webpack-Debug",
      "port": 9229,
      "skipFiles": ["${workspaceFolder}/node_modules/**/*.js"]
    }
  ]
}
```

Here we are just saying that we want to attach to the running debugging process on port 9229, and that we want to avoid debugging or stepping through the files under `node_modules`.

Another important/convient step, is to enable `Auto Attach`. You can toggle this setting on the bottom settings bar of VSCode:

![alt text](/assets/auto_attach_enabled.png "Auto attach VS Code")

This will allow you to toggle the debugger screen automatically once we execute our `node --inspect-brk` command.

### Sample Project to Debug Against

Alright, so we'll need a sample project to have Webpack bundle up for us. It's quite simple, go ahead and setup another folder outside of the forked Webpack project folder.

1.  `mkdir sample-webpack`
2.  `touch client.js`
3.  `vim client.js` -> add a few lines of code, like `console.log('Test')` etc.

That's about it! Now go back to your Webpack repo, and then we can finally run our debug commands!

### Node Inspect

Once on your Webpack repo, we'll run a quick command to bundle the `client.js` file.

Run the following command:

`node --inspect-brk bin/webpack.js --entry ./client.js --output-filename bundle.js`

This will trigger the debugger window and will break on the first line. You can then set a breakpoint on VSCode and step through the Webpack source!

![alt text](/assets/node_debug_vscode.png "Debug VS Code")

### That's it!

Go ahead and play around! If you want to do more elaborate Webpack config debug, just pass a `webpack.config.js` from your sample project like this:

`node --inspect-brk bin/webpack.js --config ./webpack.config.js`

Feel free to leave a comment below if you have any questions or any of these steps don't work for your setup.
