bst speak
=========

## Overview
The speak command generates intent requests for your service as if they were coming from Alexa itself.  
It works in a manner very similar to the Alexa simulator available via the Alexa developer console.  

To start using it, you will need a local file that contains your Intent Schema and Sample Utterances.  
By default, we have adopted the pattern used by the Alexa Skills Sample projects:
https://github.com/amzn/alexa-skills-kit-js/tree/master/samples/helloWorld

That is, we look for the Interaction Model files inside a folder called speechAssets located off the source root.  

You can specify an alternative location via options to the command-line.

 
## Speaking

To invoke the speak command, simply type:
```
$ bst speak <UTTERANCE>
```

For example:
```
$ bst speak Hello World
```

By default, the system will:
* Use the Intent Model and Sample Utterances in the speechAssets folder under the current working directory
* Use the service currently running via the `bst proxy` command

If no service is currently running via bst proxy, and HTTP endpoint can be specified with the `--url` option:
```
$ bst speak --url https://my.skill.com/skill/path Hello World
```

## Speech Asset Format and Location
If your speech assets  (Intent Model and Sample Utterances) are not stored under ./speechAssets, you can use an option to specify another location.

Example:
```
$ bst speak -i interactions/IntentModel.json -s interactions/Utterances.txt https://my.skill.com/skill/path Hello World
```

The format of these files is the same as they are entered in the Alexa Skill configuration.  
 
The Intent Schema is a JSON file. Samples utterances is a space-delimited text file.  
An example of these files is here:  
https://github.com/amzn/alexa-skills-kit-js/tree/master/samples/helloWorld

## Working With Slots
Slot handling is a bit tricky. To send an utterance that uses slots, surround the slot variables like so:  
```
{MySlot}
```

For example, if the sample utterance was defined as:
```
HelloWorld Hello world, my name is {Name}
```

Then the speak command would be:
```
$ bst speak Hello World, my name is {John}
```

The value John will then be automatically placed in the Name slot for the utterance on the request.