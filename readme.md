The FOSS pitch below, is still under construction

=======
We can translate from any Engine API to another, if we map their CONCEPT in a large public database, and that's pretty achievable with Open Source approaches.

The main architecture in most game engines is the same: start function, update loop, fixed update, events, raycast physics/colliders, play animation/sound..etc

The difference: what Unreal calls "Actor", Unity calls "Object" And Godot calls "Node", and that's what we'll be mapping.

==Challenges and solutions (Let's call the software CrossFaust):

1. Error prone, performance overhead if we use languages like Lua, with less native support  
_ We make a custom language (C style synatx for easy parsing) //.manu/Manuscript  
_ We ONLY translate .manu to files, we just need to save them in the project and most game engines will compile them,  
_ we retrieve the console log and display it in CrossFaust.  

2. Needs a massive number of API calls:  
_ We make contributions easy: a UI in the editor  
_And a cutsom file type(.adef/APIdef) in this syntax:  
```

// This is an example code, this format is designed for ease of integration

// Format: 
// # GameEngine [Plugins: libInclude1, libInclude2..]
// Basically you specify the engine, the plugin/library required if it exists, then each include required
// In case of large/complicated implementation (more than a single line) You can refernce a script for the target engine

// Be extra careful to use the exact same variable names, and specify every single one of them in each engine

#CrossFaust [Native]
Object.Move(MoveVec, MoveSpeed)

#Unity [Native: UnityEngine]
Object.GameObject.Translate(MoveVec)*Time.DeltaTime*MoveSpeed

#Unreal [Native]
Ref: ./Scripts/Transform/UnrealTranslateAPICall.cpp
```

3. Functionality X doesn't exist in Engine Y  
_ We reference a script that mimics the same behavior (like the last line in the example adef)  

4. What if it's a major feature like Nanite?  
_CrossFaust isn't supposed to replace engines, only bridge them    
_Players will not see the underlying architecture, they will see a certain art, that responds to certain clicks, with certain behaviors, we will not need Nanite, we will need lighting that looks similar to Nanite/Lumin, at a close enough performance  
_ Since we can reference scripts, we can make an antire addon, in this case: addon that takes Nanite features, and automates LODs (from an existing system or another addon), and places light probes to achieve similar looks to Nanite  

5. Architecture/philosophy/tools are different per engine and will likely cause errors  
_ True, which is why we have the option for addons, this architecture should hold up well for 80% of the redaundant tasks, the rest: we do what we'd do if we're porting from an engine to another, just automated  

6. CrossFaust cannot handle every single case in existence  
_And that's why the files/UI should be easy to read and modify,  
_Additionally, we can add whatever logging/co-devving tools we deem helpful/required  
_ CrossFaust is not supposed to automate everything, it's supposed to make 90% of your dev life easier and future proof, and give you full control to handle the remaining 10%  

========


Now, even if the pitch is appealing, we always run into the "blank project" problem in FOSS, and this project cannot be done by a single dev or even a single party.

_ The first plan is to lower the barrier to entry, which I halfway did with the .adef files format and the focus on UX (also a spreadsheet for anyone to contribute "concept" translations, like Object = Actor = Node)
_ But we still need to have a gamified system, otherwise the community will die on arrival, this is where I need you.

I'm gonna use a classic tiering system (reaction based leveling and leaderboards), but:
1. I only researched this, I never did it myself in action, so I'm very likely to bump into security mistakes (botting.. etc) that someone can be more informed than me about, I could use your help with setting it up or at least giving guidance
2. The simplest way to propell the project is the "Concepts sheet", it's what will drive momentum until the transpiler is doing something, but I need to gamify the contribution too, and spent the past 2 days looking for a bot or a bot tool combo that saves the username of the contributor, as well as recover empty fields to display as an option, there was none feasible, so I need a simple Discord bot (maybe on Replit) to handle that functionality and forward it to gamification bots


Any other recommendations, insights, opinions, questions and/or feedback are welcome.
If you feel like contributing in terms of code, management, or anything else it's also welcome and highly respectable, as the setup is not ready for easy development yet.
